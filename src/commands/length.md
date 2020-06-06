# length

**Usage**: `length[:key_type] <key>`

**Supported key types**: `bytes`, `list`, `map`, `set`, `string`

The `length` command returns the length of some bytes, a list, map, set, or
string. A key type can be specified to limit the operation to only calculating
the length of the key if it matches the specified type.

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
> length foo
2
> length:list foo
Dispatch error: the key "foo" isn't a List.
> set:set bar item1 item2 item1
item1 item2
> length:set foo
2
```
