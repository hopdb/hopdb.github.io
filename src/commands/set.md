# set

**Usage**: `set[:key_type] <key> <value...>`

**Supported key types**: `boolean`, `bytes`, `float`, `integer`, `list`, `map`,
`set`, `string`

The `set` command sets a value to a key, overriding the existing key's value if
one exists. The `set` command supports setting values of all types.

A key and value must both be provided. A key type is optional, and the default
type is raw bytes.

## Errors

If a key type is not specified then a `DispatchError::KeyUnspecified` error is
returned.

If no value is provided then a `DispatchError::ArgumentRetrieval` error is
returned.

If a provided value is of the wrong type then a
`DispatchError::KeyTypeDifferent` error is returned.

## Examples

### CLI

```
> set:bool foo true
true
> is:bool foo # "foo" is a bool
true
> set:int foo 123 # now set "foo" to an integer value of 123
123
> is:int foo # "foo" is now an integer
true
> set:list foo bar baz # now set "foo" to a list with items "bar" and "baz"
a=b
c=d
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

// set a key named "foo" to a boolean with a value of true
client.set("foo").bool(true).await?;

// "foo" is a bool
assert!(client.is(KeyType::Boolean).key("foo").await?);

// now set "foo" to an integer value of 123
client.set("foo").int(123).await?;

// "foo" is now an integer
assert!(client.is(KeyType::Integer).key("foo").await?);

// now set "foo" to a list with items "bar" and "baz"
client.set("foo").list([b"bar".to_vec(), b"baz".to_vec()]).await?;
```
