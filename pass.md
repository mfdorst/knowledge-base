# zx2c4 pass

See [passwordstore.org] for documentation.

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
