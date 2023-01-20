# Setup Git and GitHub

## Generate SSH keys
```
ssh-keygen -t ed25519
```

## Add SSH public key to GitHub

### Using gh (github-cli)
Arch: `sudo pacman -S github-cli`
Ubuntu: `sudo nala install gh`

```
gh auth login -p ssh
```

### Manually

Go to [GitHub settings](https://github.com/settings) > `SSH and GPG keys` > `New SSH key`.

Open `~/.ssh/id_ed25519.pub` and copy the contents into the key field.

Give the key a name (the name of your computer).
