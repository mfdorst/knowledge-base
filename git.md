# Git

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
