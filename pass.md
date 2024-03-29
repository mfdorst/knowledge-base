# zx2c4 pass

See [passwordstore.org] for documentation.

## Set up pass on a new computer
Create a gpg key. See [GPG](gpg.md) for instructions.

Clone the pass repo.
```
git clone git@github.com:mfdorst/pass ~/.password-store
```

Add your new public key to the public key store.
```
cd ~/.password-store
gpg --export -a new-host@mdorst.net > .public-keys/new-host.pub.gpg
echo new-host@mdorst.net >> .gpg-id
git add -A
git commit -m "Add new public key new-host@mdorst.net"
git push
```

On a device that is already authenticated, download, import, and trust the new public key.
```
cd ~/.password-store
git pull
gpg --import .public-keys/*
for key in $(ls .public-keys | sed s/\.pub/@mdorst\.net/); do
  echo "5\ny\n" | gpg --command-fd 0 --edit-key $key trust
done
```

Reencrypt all passwords with the new key, as well as all the existing keys.
```
cat .gpg-id | xargs pass init
git push
```

On the new machine, pull down the reencrypted passwords, and test that your new key works.
```
git pull
pass show aaa.com
```

Note that in order to add new passwords or update existing ones on any given device, that device
must have all public keys imported and trusted. Repeat the import and trust steps on each device
after adding a new key.

## Firefox
Install the [`passff-host`] app.
```
install-passff-host
```

Install the `passff` Firefox extension.
[Link](https://addons.mozilla.org/en-US/firefox/addon/passff/)

[passwordstore.org]: https://www.passwordstore.org/
[`passff-host`]: https://github.com/passff/passff-host
