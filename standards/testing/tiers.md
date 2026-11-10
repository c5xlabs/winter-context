# Test tiers

## Distinct test boundaries (`wctx:test-tiers`)

Each tier answers a different question. A green result at one does not substitute for another.

### Unit

One function or type in isolation. Domain decisions are tested by value, without repositories, clocks, servers, or
frameworks standing between the input and the rule. A collaborator's unit test substitutes its declared dependencies.

### Component

A coherent slice wired with real internal collaborators, with doubles at external-system seams. It proves internal
integration without claiming that a fake's interpretation of an external contract matches the real system.

### Service

The built application exercised from outside its process through its public surface. For a CLI, argv, cwd, environment,
streams, exit status, and process lifetime are real. For a server, the served protocol and running process are real.
Bind external counterparts to controlled local fixtures or mocks.

Set up service state through supported public operations. A persistence-specific case may inspect a stopped store when
the store is its explicit subject; quietly editing a running application's state bypasses the contract under test.

### UI

When the application has a UI, exercise the served or built interface in a real rendering engine. A visual claim needs a
real render of the changed surface at the widths the claim covers. A simulated DOM does not establish layout.

Recovery, concurrency, compatibility, and performance are dimensions of behavior, not extra tiers. Exercise each at the
boundaries needed to prove its promise; a crash-recovery claim needs actual interruption and restart evidence.

## Tests follow their subject (`wctx:tests-follow-the-subject`)

Make a test's tier and subject discoverable from the application's test layout. Keep the tier independently runnable and
support focused selection. The language-specific guidance chooses paths and selection syntax.

Shared fixtures and assertions live in support modules owned by their test scope, not in another collected test module.
Place a cross-concept test by the behavior it proves, not by every collaborator it uses for setup.
