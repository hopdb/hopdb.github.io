# stats

**Usage**: `stats`

**Supported key types**: none

The `stats` command returns a Map of statistics about the Hop instance. The Hop
engine maintains metrics about operations and its current state.

The following statistics are returned:

- **commands_successful**: an integer containing the number of successful
commands that have been processed.
- **commands_errored**: an integer containing the number of processed commands
that have errored.
- **sessions_started**: the number of new client sessions that have been
initiated.
- **sessions_ended**: the number of client sessions that have finished for one
reason or another.

## Errors

If a key type is specified then a `DispatchError::KeyTypeUnexpected` is
returned.

## Examples

### CLI

```python
> set:int foo 1234
1234
> stats
Commands successful: 1
Commands errored: 0
Sessions started: 0
Sessions ended: 0
```
