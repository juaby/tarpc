## 0.10.0 (2018-04-08)

## Breaking Changes
Fixed rustc breakage in tarpc-plugins. These changes require a recent version of rustc.

## 0.10.0 (2018-03-26)

## Breaking Changes
Updates bincode to version 1.0.

## 0.9.0 (2017-09-17)

## Breaking Changes
Updates tarpc to use tarpc-plugins 0.2.

## 0.8.0 (2017-05-05)

## Breaking Changes
This release updates tarpc to use serde 1.0.
As such, users must also update to use serde 1.0.
The serde 1.0 [release notes](https://github.com/serde-rs/serde/releases/tag/v1.0.0)
detail migration paths.

## 0.7.3 (2017-04-26)

This release removes the `Sync` bound on RPC args for both sync and future
clients. No breaking changes.

## 0.7.2 (2017-04-22)

## Breaking Changes
This release updates tarpc-plugins to work with rustc master. Thus, older
versions of rustc are no longer supported. We chose a minor version bump
because it is still source-compatible with existing code using tarpc.

## 0.7.1 (2017-03-31)

This release was purely doc fixes. No breaking changes.

## 0.7 (2017-03-31)

## Breaking Changes
This release is a complete overhaul to build tarpc on top of the tokio stack.
It's safe to assume that everything broke with this release.

Two traits are now generated by the macro, `FutureService` and `SyncService`.
`SyncService` is the successor to the original `Service` trait. It uses a configurable
thread pool to serve requests. `FutureService`, as the name implies, uses futures
to serve requests and is single-threaded by default.

The easiest way to upgrade from a 0.6 service impl is to `impl SyncService for MyService`.
For more complete information, see the readme and the examples directory.

## 0.6 (2016-08-07)

### Breaking Changes
* Updated serde to 0.8. Requires dependents to update as well.

## 0.5 (2016-04-24)

### Breaking Changes
0.5 adds support for arbitrary transports via the
[`Transport`](tarpc/src/transport/mod.rs#L7) trait.
Out of the box tarpc provides implementations for:

* Tcp, for types `impl`ing `ToSocketAddrs`.
* Unix sockets via the `UnixTransport` type.

This was a breaking change: `handler.local_addr()` was renamed
`handler.dialer()`.

## 0.4 (2016-04-02)

### Breaking Changes
* Updated to the latest version of serde, 0.7.0. Because tarpc exposes serde in
  its API, this forces downstream code to update to the latest version of
  serde, as well.

## 0.3 (2016-02-20)

### Breaking Changes
* The timeout arg to `serve` was replaced with a `Config` struct, which
  currently only contains one field, but will be expanded in the future
  to allow configuring serialization protocol, and other things.
* `serve` was changed to be a default method on the generated `Service` traits,
  and it was renamed `spawn_with_config`. A second `default fn` was added:
  `spawn`, which takes no `Config` arg.

### Other Changes
* Expanded items will no longer generate unused warnings.
