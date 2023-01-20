# Vim

## Search and replace

Find each occurence of `foo` (in all lines) and replace it with `bar`.
```
:%s/foo/bar/g
```

### Range modifiers
`:%s`: Search all lines instead of just one.
`:5,10s`: Search between lines 5 and 10, inclusive.
`:.,$s`: Search between current line and end of file.
`:.,+10s`: Search the 10 lines following the current one.
`:'<,'>s`: Search a visual selection. Should be automatically inserted when in visual mode.

### Search modifiers
Placed at the end, e.g. `:%s/foo/bar/gci`

`g`: Global - each occurrence in the line is changed, rather than just the first.
`c`: Ask to confirm each match.
`i`: Case insensitive.
`I`: Case sensitive.
