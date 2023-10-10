# GnuPG

## Generate a new key
```
gpg --full-gen-key
```
It is a good idea to use RSA 4096.

## Show the keys in your public key ring
```
gpg -K
```

## Show the keys in your secret key ring
```
gpg --list-secret-keys
```

## Edit your key
```
gpg --edit-key <GPG key>
```

## Export your public keys
```
gpg --export -a user@email.com > public.gpg
```

## Export your private keys
```
gpg --export-secret-key -a user@email.com > secret.gpg
```

## Import public and private keys
```
gpg --import public.gpg
gpg --import secret.gpg
```

## Trust an imported secret key
```
gpg --edit-key <GPG key> trust
> 5
> y
> quit
```
Verify it is trusted with
```
gpg --list-secret-keys
```
It should say `[ultimate]` next to your name.

## Don't ask for my password for a week

Create `~/.gnupg/gpg-agent.conf` if it does not exist, and add
```
default-cache-ttl 604800
max-cache-ttl 604800
```
After authorizing once, GPG will not ask for your password again for a week, so long as your
computer remains powered on.
