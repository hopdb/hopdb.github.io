# increment:by

**Usage**: `increment:by[:key_type] <key> <amount>`

**Supported key types**: `float`, `integer`

The `increment:by` command is a sub-command of `increment`, and like `increment`
it takes a key argument. An additional argument must be provided which specifies
the amount to increment the value by. If the key doesn't already exist, then a
default value of 0 is set and then incremented by the specified amount.

## Errors

If a key is not specified then a `DispatchError::KeyUnspecified` is returned.

If a value is not specified then a `DispatchError::ArgumentRetrieval` is
returned.

If the key type was specified and it is different than the key's type a
`DispatchError::KeyTypeDifferent` is returned.

## Examples

### CLI

```
> increment:by foo 3 # foo will be an integer since that is the default type
3
> increment:by:float foo 2.0
Dispatch error: key "foo" is not a float.
> increment:by:float bar 2.0
2.0
> increment:by bar 3.0
5.0
> increment:by foo 3
6
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

assert_eq!(3, client.increment("foo").int().by(3).await?);

// Dispatch error: key "foo" is not a float.
assert!(client.increment("foo").float().by(2.0).await.is_err());

assert!(client.increment("bar").float().by(2.0).await.is_ok());

assert!(client.increment("bar").float().by(3.0).await.is_ok());

assert_eq!(6, client.increment("foo").int().by(3).await?);
```
