# SOPS

## Generate age key
```
mkdir -p ~/.config/sops/age
age-keygen -o ~/.config/sops/age/keys.txt
```

## Add age public key to `.sops.yaml`
```
keys:
  - &primary <age-public-key>
creation_rules:
  - path_regex: secrets/secrets.yaml$
    key_groups:
      - age:
        - *primary
```

## Create a secrets file
```
mkdir secrets
sops secrets/secrets.yaml
```
