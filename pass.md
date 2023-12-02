# zx2c4 pass

See [passwordstore.org] for documentation.

## Clone existing password store
```
git clone git@github.com:mfdorst/pass ~/.password-store
gpg --import ~/.password-store/.public-keys/*
```
Create a gpg key. See [GPG](gpg.md) for instructions.

List the public keys you have imported
```
gpg --list-public-keys
```
Re-encrypt your passwords with your new key (and all of the old keys).

NOTE: You must name each of the keys that were imported in this command, or else your other devices
will lose their ability to decrypt your passwords.
```
pass init my-new-key@example.com my-old-key-1@example.com my-old-key-2@example.com ...
```
Add your new key to the password store repo
```
cd ~/.password-store
gpg --export -a my-new-key@example.com > .public-keys/my-new-key.pub.gpg
git add -A
git commit -m "Add new public key my-new-key@example.com"
git push
```

## Set up a new password store
See [GPG](gpg.md) for instructions for creating a GPG key.
```
gpg -K # Lists your GPG keys
pass init <GPG key>
pass git init
```

## Firefox
Install the [`passff-host`] app.
```
install-passff-host
```

Install the `passff` Firefox extension.
[Link](https://addons.mozilla.org/en-US/firefox/addon/passff/)

[passwordstore.org]: https://www.passwordstore.org/
[`passff-host`]: https://github.com/passff/passff-host
