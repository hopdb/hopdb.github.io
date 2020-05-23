# length

The `length` command returns the length of a Bytes, List, Map, Set, or String. A
key type can be specified to limit the operation to only calculating the length
of the key if it matches the specified type.

Usage: `length[:key_type] <key>`

CLI example:

```
> set:map foo key1 value1 key2 value2
key1=value1 key2=value2
> length foo
2
> length:list foo
Dispatch error: the key "foo" isn't a List.
> set:set bar item1 item2 item1
item1 item2
> length:set foo
2
```
