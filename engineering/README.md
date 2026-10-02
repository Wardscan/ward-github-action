# Engineering baseline index

**Supplemental draft, 2026-10-02.** Source authority:
`Wardscan/ward-github-action` at
`5cbe4c668dd443bb6a761cde8b362c503f25ccb6`, inspected statically in an isolated
worktree. This is not an approved action release, adopted policy or runtime
acceptance report. No existing shared catalog coverage is changed or claimed.

## Coverage and authority

| Required surface | Local authority |
|---|---|
| Canonical agent policy / Ready / scope / stop rules | [AGENTS.md](../AGENTS.md) |
| Thin Claude entry | [CLAUDE.md](../CLAUDE.md) |
| Thin Copilot entry / enforcement limits | [Copilot instructions](../.github/copilot-instructions.md) |
| Actual manifest/inline-script scope | [Action instructions](../.github/instructions/action.instructions.md), `applyTo: action.yml` |
| Public docs and review-aid scope | [Docs instructions](../.github/instructions/docs.instructions.md), matching Markdown paths |
| Repo-specific review packet | [PR template](../.github/pull_request_template.md) |
| Component identity / architecture / provenance | [Overview](overview.md) |
| Prerequisites / commands / verification limits | [Development](development.md) |
| Inputs / outputs / workspace / upload / compatibility | [Contracts](contracts.md) |
| Version / release / adoption / operations gates | [Delivery](delivery.md) |
| Trust boundaries / independent review / acceptance | [AI review](ai-review.md) |
| Existing consumer examples | [Inherited README](../README.md), retained, not a compatibility guarantee |

`action.yml` remains the implementation authority; these pages index that
contract rather than replace it with a new server specification. Public-facing
product/integration publication belongs in `Wardscan/ward-docs`, subject to
separate document-owner approval. Operations runbooks belong in
`Wardscan/ward-resources`, not this action repo.

## Source findings and status

The source is a Bash composite action with six declared inputs and no declared
outputs. There are no tracked workflows, tests, dependency manifests/lockfiles,
separate scripts or packaged action artifacts at the inspected revision.
The inherited README documents older action coordinates and omits required
authentication inputs; its examples have not been executed or endorsed.

The action includes Gradle/Maven/npm consumer-build branches, references
undeclared Sonar inputs, downloads an unpinned installer, leaves `registry`
unused, and does not validate mode or parse upload status for acceptance.
Token extraction and HTTP responses have no explicit validation. See
[contracts](contracts.md) for the exact observed behavior and unknowns;
these are documentation findings, not implemented fixes.

## Shared lifecycle and remaining gates

The [shared WARD baseline](https://github.com/Maggioli-Greece/issues/tree/main/docs/ward-pilot)
and its [lifecycle](https://github.com/Maggioli-Greece/issues/blob/main/docs/ward-pilot/lifecycle.md)
are proposed **UNPUBLISHED** references; no availability, adoption or enforcement
is asserted. This supplement supersedes the older action deferral only for its
approved docs scope, not the frozen review package.

[Maggioli-Greece/issues#4019](https://github.com/Maggioli-Greece/issues/issues/4019)
is a historical/illustrative example, excluded from this pilot and owned by
another developer. No implementation, reassignment, scope or status change is
authorized here; a different pilot issue remains unselected.
[Maggioli-Greece/issues#3780](https://github.com/Maggioli-Greece/issues/issues/3780)
is a separate future CI implementation task.

Named owners/reviewers, consumer contracts and formats/versions/limits/errors,
installed tool versions, build/job/settings evidence, evidence storage/retention,
publication and execution approval remain gates. Runtime, build, test, action,
scan, upload, downstream processing and deployment are **UNRUN** for this unit.
