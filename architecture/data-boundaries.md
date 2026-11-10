# Data boundaries

## Data roles (`wctx:data-roles`)

Every application-owned data type has an unambiguous role. Make the role apparent through its declaration, module
ownership, or language-specific conventions; no universal annotation syntax is required.

### Domain model

A concept the application reasons about, with or without rules. Query criteria, pages, counts, and use-case outcomes can
be domain values too. A domain model holds values, not clients, ports, clocks, or infrastructure handles.

### Boundary DTO

The application's contract with the outside: a request, response, command input, or serialized payload. It belongs at
the application boundary. Construction and representation validation can live here; business decisions belong to the
domain model, not to the transport shape.

### Adapter-private model

An outside system's representation or adapter working state, such as a table row or parsed tool payload. It stays
private to that adapter and never appears in a domain-facing port signature.

### Collaborator

A capability other code calls to do work. A type holding plain fields can still be a collaborator; a client configured
with an address is not a domain value merely because its constructor accepts only strings.

## Boundary mapping (`wctx:boundary-mapping`)

Translate DTOs to domain values where the application meets the outside, and translate adapter representations behind
their ports. A domain service does not take an HTTP request object or return a storage row. Crossing an internal port
does not turn a domain value into a DTO.

Shared vocabulary can retain its single definition across representations; it does not require duplicate enums. That
does not make a complete transport model the application's internal domain model.

## Domain operations take values (`wctx:domain-takes-values`)

Pass the loaded, typed objects a domain rule reasons about, rather than identifiers it must resolve through I/O.
Identifier parsing and lookup belong outside the pure rule. Where there is no aggregate to load, pass a typed set of the
facts the decision needs rather than inventing one.

Resolve the operation's subject at the input boundary before invoking its use-case service. A lookup that itself
evaluates a business guard can stay in the use case, with that reason explicit at the operation. A raw id is not a
substitute for an available domain concept. Generic infrastructure can take primitives honestly; do not invent domain
types for concepts the application does not model.

Loaded objects alone do not establish write-time freshness;
[external-systems/transactions.md](./external-systems/transactions.md) owns that constraint.
