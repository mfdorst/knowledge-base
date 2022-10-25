# Setup Git and GitHub

## Generate SSH keys

```
ssh-keygen -t ed25519
```

## Add SSH public key to GitHub

### Using github-cli
Install github-cli (e.g. `sudo pacman -S github-cli`)

```
gh auth login
```
### Manually

Go to [GitHub settings](https://github.com/settings) > `SSH and GPG keys` > `New SSH key`.

Open `~/.ssh/id_ed25519.pub` and copy the contents into the key field.

Give the key a name (the name of your computer).

