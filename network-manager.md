# NetworkManager

## Show status
```
nmcli
```

## List connections
```
nmcli con show
```

## Toggle connections
```
nmcli con up <connection-name>
nmcli con down <connection-name>
```
`<connection-name>` may be something like `"Wired connection 1"`.

## Change the interface for a connection
```
nmcli con mod <connection-name> connection.interface-name <interface>
```
`<connection-name>` may be something like `"Wired connection 1"`.
`<interface>` may be something like `enp8s0`.
