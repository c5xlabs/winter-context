# Contributing

## Authoring

Read `winter-canon:/principles.md`, `winter-canon:/voice.md`, and `winter-canon:/progressive-disclosure.md` before
changing governance prose or routing. Canon owns the authoring conventions; this repository owns the engineering rules
it supplies.

Keep shared rules independent of language and application topology. A concrete realization belongs in separately routed
language or application guidance, not in an exception naming one consumer inside a shared rule. A rule may be
conditional on a real concern, such as a multi-repository atomic write; it does not require applications to invent that
concern.

Every rule has a stable `wctx:<slug>` id in its heading. Define an id in one heading only and cite it elsewhere as a
bare code span. Each slug is unique across this repository; resolve an id by searching for its heading. Update the
router when adding, moving, or removing a leaf.

Document enforcement truthfully. Shared guidance does not supply application-specific architecture guards or test
fixtures: name an existing gate only where it actually runs, and record a missing gate as a gap in the application's own
verification guidance.

## Verification

Run the methods declared in [verifiability.md](./verifiability.md). New rules and changed routing also owe the cold
behavioral evaluation in `winter-canon:/evaluating-harness-changes.md` before push. Check discovery and behavior
separately; record the scenario and run count with the delivery evidence, not inside a convention.

## Delivery

Use Conventional Commits with a subsystem scope, or `winter-context` for a cross-cutting change. The default branch is
`master`. Maintainers rebase onto the current upstream before pushing; outside contributors open a pull request.
