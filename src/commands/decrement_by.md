# Decrement By

The `decrement:by` command is a sub-command of `decrement`, and like `decrement`
it takes a key argument. An additional argument must be provided which specifies
the amount to decrement the value by. If the key doesn't already exist, then a
default value of 0 is set and then decremented by the specified amount.

A key type of Float or Integer may be specified. If a different key type is
specified then an error is returned.

If a key exists of a different type than the specified key type, then an error
is returned. For example, if a Float key type is specified but a key exists
which is an Integer, then the command will error.

Usage: `decrement:by[:key_type] <key> <amount>`

CLI example:

```
> decrement:by foo 3 # foo will be an integer since that is the default type
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
