# Transaction boundaries

These rules bind operations whose correctness depends on atomicity or concurrent state. They do not require a database
or a transaction abstraction for an operation that has no such concern.

## Name the unit of work (`wctx:unit-of-work`)

When a use case must commit across repositories atomically, its orchestrator opens a named unit of work and passes its
opaque transaction to the participants. Connections and driver handles stay in adapters. A single repository's
self-contained write can own its own transaction.

## Participate in the supplied transaction (`wctx:transaction-participation`)

A participating repository uses the supplied transaction for every participating read and write. It neither opens nor
commits an independent transaction. A method correct only inside a unit requires its transaction explicitly.

Validate the transaction's owning store, scope, and lifetime. Acquire a complete required lock set before performing
participating operations, with a consistent order across writers; do not accumulate locks in an order another writer can
invert.

## Keep transactions short (`wctx:short-transactions`)

Keep locked work short and local. Do network calls outside the locked scope, including network calls hidden behind
collaborators. Re-read and validate race-sensitive state after acquiring the transaction's protection.

## Re-establish write freshness (`wctx:write-freshness`)

A decision made from an earlier read is applied only if its assumptions still hold. Use a version-conditioned write or
re-read under the operation's concurrency protection. Map a lost race to the use case's declared outcome rather than
silently applying a stale decision.

The domain owns legality; the adapter owns refusing stale writes. Neither checking a rule at the controller nor passing
a loaded object makes a later write safe by itself.

## Read a coherent snapshot (`wctx:read-snapshots`)

When a decision or exported view requires several reads to describe one coherent state, take them through a declared
snapshot or equivalent consistency boundary. A transaction name alone does not prove the required isolation; document
the store's actual guarantee. Independent reads through another connection do not join a snapshot by lexical nesting.

## Publish after commit (`wctx:publish-after-commit`)

Publish notifications about committed changes only after the unit commits. A rollback must not leave subscribers acting
on an announced write that never became durable. If delivery after a crash is part of the contract, give that delivery a
durable recovery mechanism; moving a callback after commit alone does not guarantee delivery.
