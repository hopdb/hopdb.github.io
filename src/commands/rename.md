# rename

The `rename` command renames a key by moving the value from one key to another.
The source key must have a value, and the destination key must not already be
present.

The destination key name is returned on success as confirmation.

Usage: `rename <from> <to>`

CLI example:

```
> rename
The key to rename is required.
> rename foo bar
Dispatch error: key "foo" doesn't exist.
> set:int foo 123
123
> rename foo bar
bar
> set:int foo 456
456
> rename foo bar
Dispatch error: the destination key, "bar", already exists.
```
