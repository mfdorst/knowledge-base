# Mullvad VPN

## Using the command line tool
For help exploring available commands, just run `mullvad`, or `mullvad <subcommand>` to see what
commands exist.

### Login
```
mullvad account login
```
Paste account number

### Connect/disconnect
```
mullvad connect
mullvad disconnect
```

### Autoconnect
```
mullvad autoconnect set on
```

### Enable killswitch
```
mullvad lockdown-mode set on
```

### Change relay

#### List available relays
```
mullvad relay list
```

#### Set relay by country
```
mullvad relay set us
```

#### Set relay by city
```
mullvad relay set us lax
```
