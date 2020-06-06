# is

**Usage**: `is<:key_type> <key> [keys...]`

**Supported key types**: `boolean`, `bytes`, `float`, `integer`, `list`, `map`,
`set`, `string`

The `is` command checks if all of the provided key names are of a certain key
type. If at least one key does not exist or is not the specified key type,
then `false` is returned, otherwise `true` is returned.

At least one key must be provided. A key type must also be provided.

## Errors

If a key type is not specified, then a `DispatchError::KeyTypeRequired` error is
returned.

If no arguments are provided, then a `DispatchError::ArgumentRetrieval` error is
returned.

## Examples

### CLI

```
> set:bool foo false
false
> is:bool foo # foo is a bool
true
> is:int foo # foo is not an int
false
> set:int bar 123
123
> is:bool foo bar # foo is a bool, but bar is not
false
> is:bool foo baz # foo is a bool, but baz does not exist
false
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

// set a key named "foo" to a boolean with a value of false
client.set("foo").bool(false).await?;

// foo is a bool
assert!(client.is(KeyType::Boolean).key("foo").await?);

// foo is not an int
assert!(!client.is(KeyType::Integer).key("foo").await?);

// set a key named "bar" to an integer with a value of 123
client.set("bar").int(123).await?;

// foo is a bool, but bar is not
assert!(!client.is(KeyType::Boolean).keys(&["foo", "bar"]).await?);

// foo is a bool, but baz does not exist
assert!(!client.is(KeyType::Boolean).keys(&["foo", "baz"]).await?);
```
