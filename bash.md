# Bash

## `test` operators
For an exhaustive list, `man test`. Here are some common ones.

`-z STRING` the length of `STRING` is zero

`-n STRING` the length of `STRING` is nonzero

`STRING1 == STRING2` the strings are equal

`STRING1 != STRING2` the strings are not equal

`INTEGER1 -eq INTEGER2` the numbers are equal

`INTEGER1 -ne INTEGER2` the numbers are not equal

`-e FILE` `FILE` exists

`-d FILE` `FILE` exists and is a directory

`-f FILE` `FILE` exists and is a regular file

`-h FILE` `FILE` exists and is a symbolic link (same as `-L`)

## Special variables
`$#` the number of arguments passed to a function or script

`$1` the first argument passed to a function or script. `$2` is the second, etc.

`$@` all of the arguments passed to the function or script

`${@:2}` all of the arguments passed to the function or script, except `$1`

## Script behavior directives
`set -e` if any command fails, the script will exit. If you have commands should be allowed to
fail, append `|| true` or `|| :` to prevent exit.

`set -u` treat unset variables as an error, and immediately exit

`set -o pipefail` causes a pipeline to produce a failure return code if any command errors.

`set -eo pipefail` causes the script to exit if any command, including one in a pipeline, fails.

## Iterate over an array
```
items=(item1 item2 item3)
for item in "${items[@]}"; do
    echo $item
done
```

## `mktemp`
Create a temporary file in `/tmp`
```
tmpfile=$(mktemp)
```
Create a temprary directory in `/tmp`
```
tmpdir=$(mktemp -d)
```

## Wget
`-O FILE` Write output to `FILE`

`-O-` Pipe output to stdout

## Curl
`-f` Fail fast

`-L` Follow redirects

`-o FILE` Output to `FILE`

`-o-` Pipe to stdout

`-O` Output to a file named as it is named in the URL

`-s` Hide progress meter and error messages

`-sS` Hide progress meter, but show error messages

`--proto =https` only allow https

`--tlsv1.x` forces curl to use TLS vversion 1.x or later.

## Unzip
`-d DIRNAME` unzip into `DIRNAME`

## Tar
`-xf ARCHIVE` extract files from `ARCHIVE`

`-v` List files processed. Can be specified up to `-vvv` for more verbosity.

## Chown
```
chown <user>:<group> <file>
```
`-R` recursively sets ownership inside directory
