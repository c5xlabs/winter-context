# Process fixtures

## Bound process lifetime (`wctx:bounded-process-fixtures`)

A fixture that starts a process owns its lifetime, finite startup and operation deadlines, and cleanup. It detects an
early exit, reports bounded diagnostics, and terminates and reaps the processes it owns on timeout or assertion failure.
The same ownership applies to descendants that the fixture allows the subject to create.

Use isolated working directories and an explicitly constructed environment. Supply the intended executable path rather
than accidentally resolving an operator's installed application. Include failure cases for the fixture's own lifecycle
handling so a timeout cannot strand the test run.

## Drain or capture process output (`wctx:drained-process-output`)

Route output to owned files or continuously drained streams. An unread pipe can fill and block a process that still
appears alive. Keep stdout and stderr separately observable when they are separate parts of the contract, and bound the
log excerpt emitted on a failure.

## Discover readiness from the process (`wctx:process-readiness`)

Wait for an explicit readiness signal or observable usable state, with a deadline and an early-exit check. A fixed sleep
is not readiness.

A test server binds an ephemeral port itself and publishes the endpoint it actually owns. Do not probe for a free port,
close the probe, and hand the released number to another process. When an external tool cannot publish its binding,
document the constrained fallback in the application's fixture guidance rather than presenting it as race-free.
