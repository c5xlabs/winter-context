# Repository capabilities

## Read and write capabilities (`wctx:read-write-capabilities`)

Separate a repository's read-only interface from its mutation interface. A consumer receives the narrowest capability
its job needs. A read-only projection with no mutations needs no empty write counterpart.

The implementation may satisfy both interfaces. The distinction is what authority the consumer's type grants, not
whether the implementation is split into two classes.

## Controllers are read-only (`wctx:controller-read-only`)

API and CLI controllers can resolve inputs and answer queries through read repositories. They delegate mutations to
use-case services; giving an edge a raw write capability lets it bypass the rules that justify the write.

A service method that merely forwards an unchanged read adds no domain behavior. The controller can query the read
interface directly instead.

## Repository ownership (`wctx:repository-ownership`)

A repository owns access to its facts and its external system, not the orchestration of a business operation across
other repositories. Coordinate distinct repositories through their domain-facing interfaces. An adapter does not call a
sibling adapter to mutate the sibling's facts, even when both use the same underlying store.

Use a named [unit of work](./transactions.md) when those operations must commit atomically. Sharing a transaction does
not transfer ownership of another repository's behavior.
