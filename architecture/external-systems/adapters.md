# External-system adapters

## External-system seams (`wctx:external-system-seams`)

Reach external systems through injected interfaces owned by their inner consumers. Filesystem, subprocesses, HTTP,
databases, queues, and vendor SDKs are external-system concerns. Concrete bindings are selected at composition roots;
where the product offers a choice of backend, configuration selects among those bindings.

Tests can substitute the binding without changing the operation's business rules. A production backend need not have a
second production implementation before its seam is useful, and a seam does not require a plugin registry.

## Adapter isolation (`wctx:adapter-isolation`)

An adapter owns its external library calls, representation mapping, and translation of failures to its consumer's
contract. The seam's core never imports an adapter, and one adapter does not import a sibling's implementation.

Keep an adapter's modules together behind its private boundary. Helpers genuinely shared by adapters have a separate
owner; borrowing a sibling's private helper does not make it shared. The composition root can name adapters to wire
them, but business code cannot use the root as a back door into their implementations.

## Application-owned contracts (`wctx:owned-contracts`)

A replaceable backend implements operations and outcomes the application defines. Callers do not depend on a vendor's
option vocabulary, response payload, or exception type. Backend replacement changes the binding and its translation, not
the meaning of the application's interface.

An application operation over interchangeable backends does not forward arbitrary backend flags. A deliberately
transparent launcher is a different contract: preserving another program's native invocation can be its entire purpose.
Declare that boundary explicitly rather than treating it as a domain abstraction over interchangeable backends.
