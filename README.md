# minreq
[![Crates.io](https://img.shields.io/crates/d/minreq.svg)](https://crates.io/crates/minreq)
[![Documentation](https://docs.rs/minreq/badge.svg)](https://docs.rs/minreq)
![Unit tests](https://github.com/neonmoe/minreq/actions/workflows/unit-tests.yml/badge.svg)
![MSRV](https://github.com/neonmoe/minreq/actions/workflows/msrv.yml/badge.svg)

Simple, minimal-dependency HTTP client. Optional features for:
- JSON responses (`json-using-serde`)
- Unicode domains (`punycode`)
- HTTP proxies (`proxy`)
- Percent-encoding for query parameters (`urlencoding`)
- HTTPS with various TLS implementations:
  - `https-rustls` (`https` is an alias for this)
  - `https-rustls-probe`
  - `https-native-tls`
  - `https-openssl`
    - This is based on `native-tls`, just vendoring the openssl part relevant to
      minreq.
  - `https-openssl-probe`

Without any optional features, my casual testing indicates about 148
KB additional executable size for stripped release builds using this
crate. Compiled with rustc 1.94.0, `println!("Hello, World!");` is 343
KB on my machine, where the [hello](examples/hello.rs) example is 491
KB. Both are pure Rust, so aside from `libc`, everything is statically
linked.

Note: some of the dependencies of this crate are a lot more complicated than
this library, and their impact on executable size reflects that.

## Documentation

Build your own with `cargo doc --all-features`, or browse the online
documentation at [docs.rs/minreq](https://docs.rs/minreq).

## Minimum Supported Rust Version (MSRV)

This project has a stable MSRV policy per major release, so to update this
policy, we'll need to bump minreq to a new major version.

The current major version (v4) requires **Rust 1.85**, as shipped by Debian
trixie.

The rationale for this policy is to not need to make a major version bump just
for an MSRV bump in the future, as having 1.48 set in stone for minreq v2 forced
a major version bump due to a tough incompatibility issue with a new version of
rustls (even without the rustls features enabled for MSRV builds, see
[#123](https://github.com/neonmoe/minreq/issues/123) and
[#124](https://github.com/neonmoe/minreq/pull/124)). A Debian release toolchain
is the target because building on an old-ish distro might be useful for e.g.
avoiding depending on a new version of glibc. Distributing Linux binaries is so
fun.

Any optional features might come with their own (more recent) MSRVs, so this
policy only applies to minreq without any features enabled. Check the [MSRV CI
job](.github/workflows/msrv.yml) for features that happen to currently work at
the MSRV (they will be dropped from the MSRV CI if they stop compiling).

## License
This crate is distributed under the terms of the [ISC license](COPYING.md).
