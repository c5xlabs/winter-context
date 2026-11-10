# Clean architecture

## Domain core (`wctx:domain-core`)

Business rules live in a domain core that depends on nothing outward. Frameworks, transports, persistence, and operating
system I/O sit outside it and depend inward. A rule can be exercised with plain values, without starting a server,
opening a store, or constructing a framework request.

Pure computations and pure path manipulation are not I/O. A library's role, rather than whether it ships with the
language, determines whether it belongs in the core.

## Domain and orchestration (`wctx:domain-orchestration-split`)

A concept's rules belong on its model or in pure functions in its concept module. They take loaded objects and plain
values, including the current instant when relevant, and return a decision or a domain refusal.

A use-case service orchestrates: it obtains inputs, reads the clock, calls the model, and hands the decision to a port.
A controller translates external input, resolves identifiers, invokes the use case, and maps its outcome to the external
contract. It does not decide a concept's legal transitions or perform its mutations directly.

Choosing what to load, coordinating writes, and handling a lost write race are orchestration. The adapter enforces
freshness and persistence constraints; it does not restate the business rule. A model carrying state while a service
branches on that state to decide legality is a rule in the wrong place.

## Dependency inversion (`wctx:dependency-inversion`)

The inner consumer owns the interface it needs; the outer adapter implements it. Domain code names its own port and
values, not an adapter, vendor SDK, storage row, or transport error. Replacing an adapter must not require rewriting the
rule that calls the port.

For external-system bindings, follow [external-systems/index.md](./external-systems/index.md).

## Composition roots (`wctx:composition-roots`)

Build collaborators at explicit composition roots and inject them into the code that uses them. A service does not
construct a client, acquire a store, or reach into a global service locator to find its dependencies.

A long-lived process has one composition graph with explicit lifetimes. Its served interfaces and background drivers
share the process-scoped collaborators that must agree. A short-lived command can have its own root. This requires no
particular DI container or class-based implementation.

## Narrow dependencies (`wctx:narrow-dependencies`)

A collaborator takes the capabilities it uses, not a bundle exposing the application's entire graph. Composition roots
and outer drivers may hold a bundle to wire or dispatch work; the invoked operation receives its own narrow interface.

A dependency's type should tell a reader what the operation can reach. Adding a use of another capability changes that
declared dependency, rather than silently extending what a general context object permits.
