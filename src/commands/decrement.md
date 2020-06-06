# decrement

**Usage**: `decrement[:key_type] <key>`

**Supported key types**: `float`, `integer`

The `decrement` command takes a key argument and decrements a float or integer
by 1. If the key doesn't already exist, then a default value of 0 is set and
then decremented.

## Errors

If a key is not specified, then a `DispatchError::KeyUnspecified` is returned.

If the command does not support the specified key type, then a
`DispatchError::KeyTypeInvalid` is returned.

If the type of the key is different than the specified key type, then a
`DispatchError::KeyTypeDifferent` is returned.

## Examples

### CLI

```
> decrement foo # foo will be an integer since that is the default type
-1
> decrement:float foo
Dispatch error: key "foo" is not a float.
> decrement:float bar
-1.0
> decrement bar
-2.0
> decrement foo
-2
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

assert_eq!(-1, client.decrement("foo").await?);

// Dispatch error: key "foo" is not a float.
assert!(client.decrement("foo").float().await.is_err());

assert!(client.decrement("bar").float().await.is_ok());

assert!(client.decrement("bar").float().await.is_ok());

assert_eq!(-2, client.decrement("foo").int().await?);
```
