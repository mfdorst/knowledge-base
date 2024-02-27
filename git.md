# Git

## Shallow clone

Blobless clone (recommended): clones all commits and trees, but fetches blobs on-demand.
```
git clone --filter=blob:none <repo>
```
Treeless clone: clones all commits, but fetches trees and blobs on-demand. Best if you only need
the latest version, but you still need history information.
```
git clone --filter=tree:0 <repo>
```
Shallow clone: clones only the latest commit. Smallest download size. Best if only the latest
version is needed, and history information is not needed.
```
git clone --depth=1 <repo>
```

## Setup SSH keys for GitHub

### Generate SSH keys
```
ssh-keygen -t ed25519
```

### Add SSH public key to GitHub

#### Using gh (github-cli)
Arch: `sudo pacman -S github-cli`
Ubuntu: `sudo nala install gh`
NixOS: install the `gh` package

```
gh auth login -p ssh
```

#### Manually

Go to [GitHub settings](https://github.com/settings) > `SSH and GPG keys` > `New SSH key`.

Open `~/.ssh/id_ed25519.pub` and copy the contents into the key field.

Give the key a name (the name of your computer).

## Manage remotes

### Show remote URLs
```
git remote -v
```

### Change remote URL
```
git remote set-url <upstream> <url>
```
If using SSH on GitHub, the URL format will be `git@github.com:<username>/<repo>`
