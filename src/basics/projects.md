# Projects

Hop mainly consists of 4 individual projects, which in Rust terms are called
crates. They have different use cases and require different levels of support.
For example, the [engine] runs only on no-std and environments with an allocator,
while the [server] requires the standard library and OS network primitives.

### Engine

The engine is the heart of Hop. It can run on devices that have an allocator.
It's responsible for maintaining the key state, parsing command requests,
processing them, sending responses, pub/sub and client session management, and
everything else except for networking and I/O like state persistence.

The engine is a crate that can be used like any other Rust library.

Source code: <https://github.com/hopdb/hop/tree/master/engine>

Issue tracker: [@hopdb/hop/issues/crate: engine]

### Server

The server is a light binary that concurrently manages connections and
dispatches their requests to a managed instance of the engine. When the engine
gives back a response, it is sent back to clients.

**Source code**: <https://github.com/hopdb/hop/tree/master/server>

**Issue tracker**: [@hopdb/hop/issues/crate: server]

### Client

The client is the main utility of Hop. It is an asynchronous client that
abstracts away the request and response parsing. It supports creating an
"in-memory" client that runs an instance of the engine within it, and also
supports connecting to a server instance and running requests through it.

Here's a quick example of using a client to fire up a local Hop engine,
increment a key, and then decrementing it again:

```rust
use hop::Client;

let client = Client::memory();
println!("New value: {}", client.increment("foo").await?); // value is 1
println!("New value: {}", client.decrement("foo").await?); // value is 0
```

**Source code**: <https://github.com/hopdb/hop/tree/master/client>

**Issue tracker**: [@hopdb/hop/issues/crate: client]

### CLI

The CLI is used to test commands and perform debugging on a server. It can
either create a local instance of the engine and dispatch user-provided input
to it, or connect to a server and dispatch input requests to the server.

Here's a quick example of using the CLI to test the above commands:

```
> increment foo
1
> decrement foo
0
```

**Source code**: <https://github.com/hopdb/hop/tree/master/cli>

**Issue tracker**: [@hopdb/hop/issues/crate: cli]

[@hopdb/hop/issues/crate: client]: https://github.com/hopdb/hop/issues?q=is%3Aissue+is%3Aopen+label%3A%22crate%3A+client%22
[@hopdb/hop/issues/crate: cli]: https://github.com/hopdb/hop/issues?q=is%3Aissue+is%3Aopen+label%3A%22crate%3A+cli%22
[@hopdb/hop/issues/crate: engine]: https://github.com/hopdb/hop/issues?q=is%3Aissue+is%3Aopen+label%3A%22crate%3A+engine%22
[@hopdb/hop/issues/crate: server]: https://github.com/hopdb/hop/issues?q=is%3Aissue+is%3Aopen+label%3A%22crate%3A+server%22
