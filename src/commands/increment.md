# Increment

The `increment` command takes a key argument and increments a float or integer
by 1. If the key doesn't already exist, then a default value of 0 is set and
then incremented.

A key type of Float or Integer may be specified. If a different key type is
specified then an error is returned.

If a key exists of a different type than the specified key type, then an error
is returned. For example, if a Float key type is specified but a key exists
which is an Integer, then the command will error.

Usage: `increment[:key_type] <key>`

CLI example:

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