# append

**Usage**: `append[:key_type] <key> [value...]`

**Supported key types**: `bytes`, `list`, `string`

The `append` command appends a value to a key depending on the key's type. If
the key type is a `bytes`, then the given argument will be appended to the
bytes. If the key type is a `list`, then the given argument will be appended as
a new item in the list. If the key type is a `string`, then the given argument
will be appended to the string, but *only* if the argument is valid UTF-8.

A key and value must both be provided. A key type is optional, but specifying
one will restrict the operation to the key type and error if it is different.

## Errors

If a key is not specified then a `DispatchError::KeyUnspecified` is returned.

If no value is provided then a `DispatchError::ArgumentRetrieval` is returned.

If the command does not support the specified key type then a
`DispatchError::KeyTypeInvalid` is returned.

If a provided value is of the wrong type then a
`DispatchError::KeyTypeDifferent` is returned.

## Examples

### CLI

```
> set:string foo this is a utf-8
this is a utf-8
> append:string foo  valid string! :) # note the extra space
this is a utf-8 valid string! :)
> is:string foo # "foo" is a string
true
> set:list bar item1 item2
item1
item2
> append bar item3 # `append` will append "item3" to the key regardless of its type
item1
item2
item3
```

### Client

```rust
use hop::{Client, KeyType};

let client = Client::memory();

// set a key named "foo" to a string
client.set("foo").str("this is a utf-8").await?;

client.append("foo").str(" valid string! :)").await?);

// "foo" is a string
assert!(client.is(KeyType::String).key("foo").await?);

client.set("foo").list(&[b"item1".to_vec(), b"item2".to_vec()]).await?;

// `append` will append "item3" to the key regardless of its type
client.append("foo").value("item3").await?;
```
