# winter-context

**Shared engineering conventions for Winter and Blizzard applications** — the guidance an agent builds against and a
reviewer uses to judge the result.

Keeping the shared conventions in one repository lets applications build on the same engineering foundation without
maintaining their own copies. It derives from [winter-canon](https://github.com/paul-gross/winter-canon), which governs
how agent context is written and organized; this repository supplies the conventions for application code and tests.

## Start here

[`index.md`](./index.md) is the front door. Follow the route matching the change you are designing, implementing, or
reviewing rather than reading the whole tree.

| Directory                                | When to read                                                            |
| ---------------------------------------- | ----------------------------------------------------------------------- |
| [architecture/](./architecture/index.md) | Deciding where behavior belongs or how a boundary should work           |
| [standards/](./standards/index.md)       | Writing tests or judging whether they establish the behavior they claim |

## How applications use it

An application's canonical context points to this repository's entry point. That context can live in a separate
`{name}-context` repository or in the application's own `./context`; the workspace operator chooses the locations and
makes this repository and `winter-canon` available.

The workspace keeps the shared context current. Applications consume that context rather than pinning, fetching, or
placing governance copies themselves. Each application adopts it deliberately: making the repository available does not
migrate existing consumers or retire their context.

Rules carry stable `wctx:` ids so guidance, source comments, and review findings can name the convention they rely on.
[`CONTRIBUTING.md`](./CONTRIBUTING.md) owns the citation scheme.

## What stays with the application

Shared conventions are not a complete application harness. The application's context describes its own domain and
concrete architecture, and supplies the verification methods, workflows, and reference implementations that go with its
code. `winter-canon:/harness-structure.md` defines the expected shape of that harness.

Language- and application-specific guidance has its own routes. The shared rules do not choose a DI framework, test
runner, class syntax, or directory spelling for every consumer.

## Contributing

Changes target a convention directly. Read [`CONTRIBUTING.md`](./CONTRIBUTING.md) before editing and
[`verifiability.md`](./verifiability.md) for the checks that verify this repository itself, rather than an application
that consumes it.

## License

Functional Source License 1.1 with an Apache License 2.0 future license. See [LICENSE](./LICENSE).
