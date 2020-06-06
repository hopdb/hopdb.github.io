# exists

**Usage**: `exists <key> [keys...]`

**Supported key types**: none

The `exists` command checks if all of the provided key names exist. If at least
one key does not exist, then `false` is returned, otherwise `true` is returned.

At least one key must be provided, up to the global limit of 255. If you need to
check that more exist, use multiple commands.

## Errors

If a key type is specified then a `DispatchError::KeyTypeUnexpected` is
returned.

If no key is provided then a `DispatchError::ArgumentRetrieval` is returned.

## Examples

### CLI

```
> set:bool foo false
false
> exists foo
true
> set:map bar a b c d
a=b
c=d
> exists foo bar
true
> exists foo bar baz
false
```
