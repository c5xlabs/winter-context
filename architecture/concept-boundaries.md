# Concept boundaries

## Concept packages (`wctx:concept-packages`)

Group behavior by the domain concept it serves and name the grouping for that concept. A reader should be able to find a
behavior from its name without first learning the framework. Technical layers can exist within a concept; unrelated
concepts do not share a bucket merely because their files have the same technical role.

Create boundaries for concepts the application actually has. Empty product modules and speculative shared abstractions
do not establish an architecture.

## Concept dependency graph (`wctx:concept-dependency-graph`)

Declare the allowed dependencies between concept packages in an acyclic graph. A cross-concept dependency needs an
explicit edge; an edge exists because code uses it, not because a package might need it later. Remove unused edges.

An import hidden behind a type-only condition, deferred load, or local function still creates a dependency. A cycle is
resolved by moving a shared concept lower or coordination higher, not by hiding when the import occurs.

Enforce dependency direction and private boundaries through the language's visibility mechanisms or repository-owned
architecture checks. Where a custom check supplies enforcement, prove that a deliberate forbidden crossing fails it. The
application's guidance owns its concrete graph and the verification method that checks it.

## Internal visibility (`wctx:internal-visibility`)

A concept's adapter implementations and private helpers are private to that concept. Siblings depend on its public
surface. Composition roots may name concrete adapters to wire them; tests may inspect internals as white-box clients.
Neither privilege makes those internals a public API.

Use the language's native encapsulation mechanism. A directory named `internal` is one realization, not a required
cross-language spelling.

## Shared kernel (`wctx:shared-kernel`)

A shared kernel contains vocabulary and pure rules that its consumers genuinely share. It depends on neither consumer's
application-specific code. Shared vocabulary has one definition; do not maintain mirrors and conversion functions for
the same concept on each side.

A rule belongs in the kernel when multiple consumers must evaluate it identically. A rule only one consumer applies
stays with that consumer. Kernel rules take values, never I/O collaborators. A wire format is governed separately from
the shared vocabulary it carries; follow [data-boundaries.md](./data-boundaries.md) when crossing that boundary.
