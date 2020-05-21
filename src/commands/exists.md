# exists

The `exists` command checks if all of the provided key names exist. If at least
one key does not exist, then `false` is returned, otherwise `true` is returned.

At least one key must be provided, up to the global limit of 255. If you need to
check that more exist, use multiple commands.

Usage: `exists <key> [keys...]`

CLI example:

```
> set foo:bool false
false
> exists foo
true
> set bar:map a b c d
a=b
c=d
> exists foo bar
true
> exists foo bar baz
false
```
