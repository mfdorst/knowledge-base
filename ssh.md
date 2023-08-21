# Set up SSH

## Generate new SSH key
```
ssh-keygen -t ed25519
```

This will generate two files, both in `~/.ssh`. `id_ed25519`, and `id_ed25519.pub`.

**_Never share the contents of `id_ed25519` between computers._**

The `.pub` file contains your SSH public key, and that can be safely shared between computers.
Other computers can use that key to verify your identity.

## Set up public key authentication
```
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@host
```

You should now be authenticated on the remote system. Try `ssh user@host`.
You should be able to log in with no password.
