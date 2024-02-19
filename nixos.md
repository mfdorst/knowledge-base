# NixOS

## Compare nix profiles
Use `nvd` to compare package versions between profiles
```
nvd diff /nix/var/nix/profiles/system-<number>-link /run/current-system
```
Use `nix-diff` to do in-depth comparisons between derivations
```
nix-diff /nix/var/nix/profiles/system-<number>-link /run/current-system --color=always | less
```
