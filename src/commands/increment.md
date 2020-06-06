# increment

**Usage**: `decrement[:key_type] <key>`

**Supported key types**: `float`, `integer`

The `increment` command takes a key argument and increments a float or integer
by 1. If the key doesn't already exist, then a default value of 0 is set and
then incremented.

## Errors

If a key is not specified, then a `DispatchError::KeyUnspecified` is returned.

If the command does not support the specified key type, then a
`DispatchError::KeyTypeInvalid` is returned.

If the type of the key is different than the specified key type, then a
`DispatchError::KeyTypeDifferent` is returned.

## Examples

### CLI

```
> increment foo # foo will be an integer since that is the default type
1
> increment:float foo
Dispatch error: key "foo" is not a float.
> increment:float bar
1.0
> increment bar
2.0
> increment foo
2
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

assert_eq!(1, client.increment("foo").await?);

// Dispatch error: key "foo" is not a float.
assert!(client.increment("foo").float().await.is_err());

assert!(client.increment("bar").float().await.is_ok());

assert!(client.increment("bar").float().await.is_ok());

assert_eq!(2, client.increment("foo").int().await?);
```
