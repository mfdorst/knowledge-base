# Battle.net on Linux (Faugus launcher)

## Fix update error "We tried to make a file writable but failed" (BLZBNTAGT00001389 / error 000030273)

Symptom: clicking Update in Battle.net fails with either a generic "Whoops! Looks like
something broke" (error code `BLZBNTAGT00001389`) or a more specific "We tried to make a
file writable but failed. Please log in as administrator and try again" (article
`000030273`).

Cause: Wine stores the Windows security descriptor (ACL) for each file in the
`user.wine.sd` extended attribute. If that attribute gets into a bad state for some files
under the game install (e.g. `Data/indices/*.index`), Wine's `SetNamedSecurityInfo` calls
fail, and the Agent can't clear the Windows "read-only" flag before patching, even though
the underlying Linux file permissions are fine. Check the Agent's error log to confirm:

```
grep -i -E "error|fail|denied|exception" ~/Faugus/battlenet/drive_c/ProgramData/Battle.net/Agent/Agent.<version>/Logs/AgentErrors-<timestamp>.log | tail -50
```

Look for lines like:

```
fix_permissions path="..." failed to remove read only flag from file attributes
AgentAsAdmin failed to fix the file permissions of '...'
```

Fix: strip the stale `user.wine.sd` xattr from the affected files so Wine regenerates a
fresh one. Across the whole WoW install:

```
find ~/Faugus/battlenet/drive_c/"Program Files (x86)"/"World of Warcraft" -exec setfattr -x user.wine.sd {} \; 2>/dev/null
```

Then relaunch Battle.net and retry Update.

Also worth doing first/alongside, in case plain Unix permissions are the issue too:

```
find ~/Faugus/battlenet/drive_c/"Program Files (x86)"/"World of Warcraft" -type f -exec chmod u+w {} \;
find ~/Faugus/battlenet/drive_c/"Program Files (x86)"/"World of Warcraft" -type d -exec chmod u+rwx {} \;
```

### Getting real error output from Battle.net (not just the popup)

Faugus launches Battle.net through `umu-run`, not plain `wine` — running plain `wine`
against the prefix throws a `wine client error: version mismatch` because the prefix was
set up for a different Proton/GE build. To launch with visible terminal output, find the
Proton path Faugus is using (look for a `toolmanifest.vdf`):

```
find ~ -iname "toolmanifest.vdf" 2>/dev/null
```

Then launch directly:

```
WINEPREFIX=~/Faugus/battlenet GAMEID=battlenet PROTONPATH="<path to Proton build>" umu-run "~/Faugus/battlenet/drive_c/Program Files (x86)/Battle.net/Battle.net.exe"
```

Battle.net's own Agent logs (more useful than terminal output, which usually stays silent
even on failure) live at:

```
~/Faugus/battlenet/drive_c/ProgramData/Battle.net/Agent/Agent.<version>/Logs/
```

Key files per session (`<timestamp>` matches across a set):
- `AgentErrors-<timestamp>.log` — actual errors, check this first
- `Agent-<timestamp>.log` — full agent log
- `AgentUpdate-<timestamp>.log` — update-specific log

Note: you'll also see many `SetNamedSecurityInfo`/`GetNamedSecurityInfo` errors for
essentially every file scanned (including things like addon folders) — this is routine
Wine ACL noise, not the actual failure. The real cause is usually a `fix_permissions`
error, which is much rarer in the log.
