# decrement:by

**Usage**: `decrement:by[:key_type] <key> <amount>`

**Supported key types**: `float`, `integer`

The `decrement:by` command is a sub-command of `decrement`, and like `decrement`
it takes a key argument. An additional argument must be provided which specifies
the amount to decrement the value by. If the key doesn't already exist, then a
default value of 0 is set and then decremented by the specified amount.

## Errors

If a key is not specified then a `DispatchError::KeyUnspecified` is returned.

If an argument is not provided, then a `DispatchError::ArgumentRetrieval` is
returned.

If a key type is specified but the value of the key is of a different type, then
a `DispatchError::KeyTypeDifferent` is returned.

## Examples

### CLI

```
> decrement:by:int foo 3
-3
> decrement:by:float foo -2.0
Dispatch error: key "foo" is not a float.
> decrement:by:float bar -2.0
-2.0
> decrement:by bar -3.0
-5.0
> decrement:by foo -3
-6
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

assert_eq!(-3, client.decrement("foo").int().by(3).await?);

// Dispatch error: key "foo" is not a float.
assert!(client.decrement("foo").float().by(2.0).await.is_err());

assert!(client.decrement("bar").float().by(2.0).await.is_ok());

assert!(client.decrement("bar").float().by(3.0).await.is_ok());

assert_eq!(-6, client.decrement("foo").int().by(3).await?);
```
