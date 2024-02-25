# Minecraft

## Enable the HTTP API in ComputerCraft:

_Note: The server will overwrite this setting when it stops, so make sure to stop the server, then
change the setting, then start it again, otherwise your setting will be overwritten._

`world/serverconfig/computercraft-server.toml`
```
[http]
    enabled = true
```
To make it the default in all worlds, set it in `defaultconfig/computercraft-server.toml`.

## Increase chunkload max
`world/serverconfig/ftbchunks-world.snbt`
```
max_claimed_chunks: 5000
max_force_loaded_chunks: 1000
```
Or whatever values you want.
