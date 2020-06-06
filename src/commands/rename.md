# rename

**Usage**: `rename <from> <to>`

**Supported key types**: none

The `rename` command renames a key by moving the value from one key to another.
The source key must exist, and the destination key must not already be taken.

The destination key name is returned on success as confirmation.

## Errors

If a key type is specified then a `DispatchError::KeyTypeUnexpected` is
returned.

If a source key is not specified then a `DispatchError::KeyUnspecified` is
returned.

If a destination key is not specified then a `DispatchError::ArgumentRetrieval`
is returned.

If the source key does not exist then a `DispatchError::KeyNonexistent` is
returned.

If the destination key does not exist then a `DispatchError::PreconditionFailed`
is returned.

## Examples

### CLI

```
> rename
The key to rename is required.
> rename foo bar
Dispatch error: key "foo" doesn't exist.
> set:int foo 123
123
> rename foo bar
bar
> set:int foo 456
456
> rename foo bar
Dispatch error: the destination key, "bar", already exists.
```
