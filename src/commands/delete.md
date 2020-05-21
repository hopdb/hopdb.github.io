# delete

The `delete` command deletes a key by name. A key type can't be specified, and
regardless of type the key will be deleted if it exists. The key's name is
returned on success as confirmation.

Usage: `delete <key>`

CLI example:

```
> set foo:list item1 item2 item1
item1
item2
item1
> exists foo
true
> delete foo
foo
> exists foo
false
```
