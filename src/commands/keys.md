# keys

**Usage**: `keys[:key_type] <key>`

**Supported key types**: `map`

The `keys` command returns a list of all of the keys of a map. For example, a
map with the key-value pair `key1` and `value1` and a second key-value pair of
`key2` and `value2`, when retrieved with this command will return a list with
`key1` and `key2`.

## Errors

If a key is not specified then a `DispatchError::KeyUnspecified` is returned.

If a specified key type is not supported than a `DispatchError::KeyTypeInvalid`
is returned.

If the specified key does not exist thyen a `DispatchError::KeyNonexistent`
is returned.

If the key type of the key is different than the specified key type then a
`DispatchError::KeyTypeDifferent` is returned.

## Examples

### CLI

```
> set:map foo key1 value1 key2 value2
key1=value1 key2=value2
> keys foo
key1
key2
> set:map bar key value
key=value
> keys bar
key
```
