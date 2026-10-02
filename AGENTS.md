# Ward GitHub Action agent policy

Canonical policy for agents working in `Wardscan/ward-github-action`.
Supplemental documentation draft, 2026-10-02; human adoption is pending.

## Purpose and source authority

This repository contains a GitHub composite action, not a Java service or a
Node-based action. [action.yml](action.yml) is both its manifest and its inline
Bash entry point. It installs Syft, optionally invokes consumer build tooling,
generates `sbom.json`, and attempts asset synchronization. The inherited
[README](README.md) contains older Mitigate usage examples; preserve that content
and use the [engineering index](engineering/README.md) for observed limitations.

The [contract index](engineering/contracts.md) describes actual inputs, absent
outputs, workspace behavior and upload/error handling. Do not infer supported
versions, accepted server formats or successful delivery from names/descriptions.
Keep consumer build/test evidence separate from scanning and uploading, even
though the current action includes build branches.

## Ready and bounded work

Start from an approved packet containing a canonical issue/spec reference,
acceptance cases, accountable task owner, independent human reviewer, target
repo/base SHA, allowed paths, non-goals, dependencies, data classification,
verification commands and execution/publication limits. Use justified N/A for
irrelevant surfaces; record an owner and next action for unknowns.

Use one writer per repository and branch in an isolated worktree. Check initial
status, read inherited instructions, and preserve staged, unstaged and untracked
work. Do not access or modify the primary checkout or another writer's worktree.
Do not turn a component supplement into shared catalog/process edits.

For this supplemental unit, only documentation, agent instructions, a local PR
checklist and an additive README pointer are authorized. No source, manifest,
workflow, configuration, dependency or toolchain changes. No commit, push, PR,
issue/settings/job changes, dependency installation, scripts, actions, builds,
tests, scans, downloads, token use, uploads, network queries or deployment.
[Maggioli-Greece/issues#3780](https://github.com/Maggioli-Greece/issues/issues/3780)
is separate future implementation, not authority for action or workflow changes.

## Verification and evidence

Use offline text/source/link/anchor/frontmatter/glob/allowed-path checks for this
unit. Read every new file: Git diff alone excludes untracked additions. Check
that source and inherited content remain intact. Record exact source revision,
changed paths, performed checks, results and skipped checks with reasons.

For later authorized code work, follow [development](engineering/development.md)
and update the affected input/output/error/version contracts, consumer examples,
docs and evidence together. Do not introduce a parallel API specification or
pretend a new workflow/check is already enforced. Static inspection is not
runtime success; HTTP 2xx or an uploaded SBOM is not build, test, deployment,
completed processing or acceptance evidence.

## Trust, review and stop conditions

Public docs must not contain credentials, token/response dumps, customer SBOMs,
private source excerpts, internal addresses or deployment topology. Do not read
secret files or reuse live credentials. Trusted workflow/action references and
checked-out source are separate trust boundaries: untrusted pull-request content
must not be executed with privileged credentials. See [review](engineering/ai-review.md).

Stop and report an actionable blocker for conflicting work, missing approvals,
unsafe data/credential boundaries, unresolved consumer contracts, incompatible
versions or unknown required owners. Do not guess formats, limits, active UI,
runtime results or enforcement. Escalate repeated failed corrections rather
than expand scope.

Independent human review is required; agents do not approve their own work.
Review, merge, action publication, consumer adoption, runtime acceptance and
deployment require separate decisions. See [delivery](engineering/delivery.md).

## Shared authority

The shared [WARD lifecycle](https://github.com/Maggioli-Greece/issues/blob/main/docs/ward-pilot/lifecycle.md)
is a proposed **UNPUBLISHED** baseline, not an active check or public dependency.
Do not copy restricted process/core material here. Product documentation belongs
in `Wardscan/ward-docs`; operational runbooks belong in `Wardscan/ward-resources`.
The current scripts-agent role is `Wardscan/ward-agent-dev` (user-confirmed,
deployment/version unverified); deprecated `Wardscan/ward-agent` is not a target.
These role references confer no permission for cross-repository changes.
