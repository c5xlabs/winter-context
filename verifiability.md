# Verifying winter-context

These methods verify this governance repository, not the applications that consume its rules. Each consuming application
owns its concrete verification matrix under `winter-canon:/verifiability-matrix.md`.

## Commands

Run from this repository's worktree root.

| Method                           | Command                         |
| -------------------------------- | ------------------------------- |
| `winter-context:markdown-format` | `npx --yes dprint@0.55.2 check` |
| `winter-context:markdown-lint`   | `uvx rumdl@0.2.54 check .`      |

The tools require network access on first acquisition and use their caches afterward. Formatting is applied with
`npx --yes dprint@0.55.2 fmt`.

## Manual testing

### References (`winter-context:manual-references`)

Starting from [index.md](./index.md), follow every routing branch. Check that every rule leaf is reached, every local
link and anchor resolves, and every `wctx:` citation has exactly one defining heading.

Resolve foreign canon references against the operator's available `winter-canon`. Check that shared rules carry no
consumer-specific paths, language-specific mandates, or claims that an application gate already exists. A pass leaves no
broken reference, unreachable rule, duplicate definition, or misleading enforcement claim.

### Behavior (`winter-context:manual-cold-eval`)

Use `winter-canon:/evaluating-harness-changes.md` for a new rule or changed routing. Give fresh agents realistic tasks
through this repository's entry point, without naming the rule being tested. Observe whether each agent reaches the
relevant leaf and applies it correctly, including clean counterexamples. Both discovery and behavior must pass; record
the scenario, separate verdicts, and run count with the delivery evidence.

## Tools

`tool:governance-context` — the operator makes `winter-canon` available to resolve its path references. Governance
checks need no running application, database, or application provisioning. No application lifecycle command is supplied
by this repository.
