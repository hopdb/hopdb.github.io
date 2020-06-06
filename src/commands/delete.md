# delete

**Usage**: `delete <key>`

**Supported key types**: none

The `delete` command deletes a key by name. A key type can't be specified, and
regardless of type the key will be deleted if it exists. The key's name is
returned on success as confirmation.

## Errors

If a key type is specified then a `DispatchError::KeyTypeUnexpected` is
returned.

If a key is not specified then a `DispatchError::KeyUnspecified` is returned.

If the key does not exist then a `DispatchError::PreconditionFailed` is
returned.

## Examples

### CLI

```
> set:list foo item1 item2 item1
item1
item2
item1
> exists foo
true
> delete foo
foo
> exists foo
false
```
