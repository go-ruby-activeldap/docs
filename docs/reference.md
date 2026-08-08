# Reference

The public API lives at the module root (`github.com/go-ruby-activeldap/activeldap`). It is
**Ruby-shaped but Go-idiomatic**: names mirror Ruby's `activeldap`, while the surface
follows Go conventions — value types, explicit errors, no global state.

## Install

```sh
go get github.com/go-ruby-activeldap/activeldap
```

## Import

```go
import "github.com/go-ruby-activeldap/activeldap"
```

## Connection setup

The mapper speaks to a directory over a Net::LDAP connection: a host, port, bind
DN and credentials, and a base DN. Configure the connection once, then map object
classes against that base DN and run `find` / `search` / CRUD through it. The
connection surface mirrors reference `activeldap`'s `ActiveLdap::Base.setup_connection`.

## API reference

The authoritative, always-current API reference is generated from the source by
pkg.go.dev:

- **[pkg.go.dev/github.com/go-ruby-activeldap/activeldap](https://pkg.go.dev/github.com/go-ruby-activeldap/activeldap)**

The module's [README](https://github.com/go-ruby-activeldap/activeldap#readme) carries worked
examples — mapping an object class, `find`/`search`, create/update/destroy,
validations, associations and LDIF — and the full, up-to-date surface. This page
intentionally links to those canonical sources rather than duplicating signatures
that could drift out of date.

## Conformance

Behaviour is pinned by a **differential oracle** against reference Ruby: a corpus
of mappings, filters, DN compositions, validations and LDIF round-trips is run
through both the `ruby` binary (with the `activeldap` gem, against a test directory)
and this library, and the results are compared — gated on the reference where
relevant and skipping itself where `ruby` is absent so the cross-arch lanes still
validate the library.
