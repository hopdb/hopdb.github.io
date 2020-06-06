# type

**Usage**: `type <key>`

**Supported key types**: none

The `type` command retrieves the key type of a key.

At least one key must be provided. A key type must also be provided.

## Errors

If a key is not specified, then a `DispatchError::KeyUnspecified` is returned.

If a key type is specified then a `DispatchError::KeyTypeUnexpected` is
returned.

If the key does not exist then a `DispatchError::KeyNonexistent` is returned.

## Examples

### CLI

```
> set:bool foo true
true
> type foo
bool
> set:int bar 123
123
> type bar
int
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

client.set("foo").bool(true).await?;
assert_eq!(KeyType::Boolean, client.key_type("foo").await?);

client.set("bar").int(123).await?;
assert_eq!(KeyType::Integer, client.key_type("bar").await?);
```
