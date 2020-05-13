# Installation

HopDB is available through Cargo and Docker.

## Cargo

```sh
$ cargo install hop
$ PORT=14000 cargo hop
```

### Docker

Run an instance of the latest version of HopDB, bound to port 46733 on the host:

```sh
$ docker run -p 46733:46733 vzlh/hop
```
