# Test isolation

## Hermetic tests (`wctx:hermetic-tests`)

Automated gating tests do not spend real vendor tokens, require personal credentials, or contact uncontrolled remote
systems. Bind those seams to explicit fakes, local fixtures, or mock counterparts with deterministic failure levers.
Real-I/O adapter checks use disposable local resources; separately declared live integration checks state their setup,
cost, and limits rather than silently joining the hermetic suite.

Give cases isolated state, including temporary files, mutable stores, environment variables, and application caches.
Parallel runs must not borrow an operator's home, workspace, or installed configuration as a fixture.

## Resources end with their owner (`wctx:owned-test-resources`)

A test-created resource belongs to its creating test or fixture scope. Stop its users before releasing it, close open
handles before removing backing files, and clean up on failure as well as success. Shared helpers participate in that
cleanup instead of requiring each caller to remember it.

Borrowed resources remain their owner's responsibility. An expensive shared fixture must preserve isolation and stay
usable until its final borrower finishes; a test cannot dispose it early to simplify its own cleanup.

## Control domain time (`wctx:controlled-domain-time`)

Time-dependent business behavior receives time through an injected clock or as plain instant values. Tests advance a
controlled domain clock and drive the relevant operation rather than waiting for a real business interval to elapse.

Mechanical deadlines use monotonic elapsed time. Advancing domain time must not disable a process timeout or make a
readiness wait expire. Control shared clocks only within a fixture scope that owns all affected users.

## Keep mock contracts aligned (`wctx:mock-contract-parity`)

A changed external contract updates its controlled counterpart and the cases that exercise it in the same coordinated
change. A fake that only repeats an expected call shape cannot prove the real binding still works.

Supplement seam-level tests with adapter checks against the actual local tool or library where format and version drift
matter. Treat real remote-system checks as the separately declared live integrations described above, not as evidence
the hermetic mock already provides.
