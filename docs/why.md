# Why pure Go

`go-ruby-activeldap/activeldap` reimplements Ruby's `activeldap` in **pure Go, with cgo
disabled**. The slice of Ruby it covers is **deterministic and
interpreter-independent**: the object–LDAP mapping — how object classes, attributes,
DNs, filters, validations and LDIF are shaped — is a pure function of its inputs
and the directory it talks to. The live piece, the directory connection itself,
is a Net::LDAP client; everything above it is exactly the part that can — and
should — live as a standalone Go library, separate from the interpreter.

## Extracted for reuse, reusable by anyone

- any Go program can import `github.com/go-ruby-activeldap/activeldap` directly, with no
  Ruby runtime, to talk to an LDAP directory the ActiveRecord way;
- the dependency runs the *other* way — `rbgo` binds this module as a native
  module for [go-embedded-ruby](https://github.com/go-embedded-ruby/ruby) (the same
  pattern as [go-ruby-yaml](https://github.com/go-ruby-yaml/yaml)), rather than
  this module depending on the interpreter;
- the behaviour is pinned by a **differential oracle** against reference Ruby,
  independent of any one consumer.

## Why pure Go matters here

Because the library is CGO-free, it:

- cross-compiles to every Go target with no C toolchain, and links into a single
  static binary;
- has **no dependency on the Ruby runtime** — the dependency runs the other way;
- can be differentially tested against the `ruby` binary wherever one is on
  `PATH` (against a test directory), while the cross-arch lanes still validate the
  mapping, filter-building and LDIF logic itself.

See [Reference](reference.md) for the import path and API.
