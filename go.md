# Go

## Move default go directory
By default, go installs binaries in `~/go/bin`. This is quite an annoying place for it, so you may
want to move it.

In your `.zshrc` or `.bashrc`
```
export PATH="$HOME/.go/bin:$PATH"
export GOPATH="$HOME/.go"
```
If you already have things installed in `~/go/bin`, you will need to move it.
```
mv ~/go ~/.go
```

## Run a go server and watch for changes
```
go install github.com/mitranim/gow@latest
gow run .
```


