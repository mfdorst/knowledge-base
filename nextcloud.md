# Nextcloud gotchas

## Troubleshoot Failed Install

Check if there are existing files from a previous install

`/var/lib/nextcloud`, `/var/lib/redis-nextcloud`, `/var/lib/postgresql`, etc.

Removing these directories may help. **Be careful, deleting these could result in data loss.**
