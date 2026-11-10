# Test evidence

## Assertions observe their claims (`wctx:assertions-observe-claims`)

Claim only what the assertion actually observed. A case's own body must establish what its name promises; a sibling's
coverage does not make a copied body prove a different outcome.

An idempotency case performs the operation twice and re-reads the resulting state. A boundary case observes the
boundary's effect, not merely a call to an internal helper. Assertions should fail when the promised behavior breaks,
not just confirm the fixture was configured.

## Wait on causal progress (`wctx:causal-waits`)

Wait for an event, readable state, completed pass, or other causal barrier. For a negative assertion, establish that the
system reached the point where a forbidden effect would have occurred before asserting its absence. A barrier must still
be reachable when the behavior is correctly suppressed.

Immediate absence and a sleep shorter than the subject's cadence prove nothing about eventual behavior. When elapsed
business time is the subject, advance the controlled clock and drive the operation that judges it.

## Prove regression sensitivity (`wctx:regression-sensitivity`)

For a load-bearing new decision or repaired defect, demonstrate that the intended assertion detects the wrong behavior:
run it against the pre-fix behavior or a deliberate mutation of that decision. Restore the production code afterward. A
repository's mutation tooling can broaden this check; no particular mutation runner is required.

An aggregate red caused by an unrelated assertion is not evidence. Name which assertion failed and why that failure
matches the claim. A custom architecture guard likewise needs a deliberate violating fixture that proves detection.

## Gating checks exercise production paths (`wctx:gating-production-paths`)

The checks required to land a change exercise its production path, including configuration wiring and the binding used
in production. A convenient test-only route cannot substitute for that path. Non-gating journeys can add confidence, but
do not protect behavior the landing checks never drive.

Use the application's declared verification methods when claiming completion. A narrowed development run is useful
feedback, not a claim that the full declared method passed. Record unavailable methods and uncovered behavior as gaps.
