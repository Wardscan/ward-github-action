# Delivery and operations boundaries

[Index](README.md) | [Contracts](contracts.md) | [Review](ai-review.md)

## Native delivery model

This is a composite action consumed through a Git repository ref and
`action.yml`; no action binary, container image, compiled bundle or package
publication pipeline is tracked at source revision
`5cbe4c668dd443bb6a761cde8b362c503f25ccb6`. There are no tracked repository
workflows or release/test jobs. External jobs, tags/releases, settings, installed
versions, required checks and current consumers are unknown and were not queried.

Consumer application builds, produced artifacts, tests and deployments are
separate from releasing/adopting this action. Current embedded Gradle/Maven/npm
commands are documented exceptions, not proof that a scan/upload proves a
consumer build or that the separation is already implemented.

## Evidence chain and independent gates

| Stage | Evidence/approval needed for future authorized work |
|---|---|
| Source review | Exact action revision, scoped diff, approved spec/consumer contract, independent review and recorded findings |
| Action verification | Approved runner/tool matrix, isolated fixture revisions, actual performed checks and error/compatibility cases; unrun checks remain explicit |
| Publication | Approved immutable action SHA and reviewed release/version/ref mapping; no tag or semantic-version policy is inferred |
| Consumer adoption | Trusted workflow revision and action pin, checkout revision, least-privilege permissions and compatible runner/scanner/build/service versions |
| Consumer build/test | Separate commands/reports, source identity, artifact digest and test results; scanning and HTTP status are not substitutes |
| SBOM/upload | Exact scan target, scanner/version/schema and SBOM digest; sanitized authentication/HTTP evidence only if execution is approved |
| Downstream acceptance | Owner-agreed asset association and processing/result evidence, with approved formats/limits/errors and acceptance cases |
| Deployment/operations | Separate consumer deployment approval, artifact/config/target evidence, health/rollback acceptance; not an action responsibility by default |

The Syft installer is fetched from upstream `main`, with no version/checksum pin
here. Inherited README examples use action `@main` and dependency major refs.
Review future immutable pins and version compatibility with owners; do not
change refs or claim reproducibility in this docs-only unit.

## Rollback, monitoring and retention

For a future approved release, an owner must identify a reviewed prior action
SHA and compatible consumer workflow/tool/service revisions. Rollback normally
means an approved consumer ref/config change, not deploying a pretend HTTP
service for this repo. No automatic rollback mechanism is present.
Reverting the action ref does not undo remote uploads, installed tooling,
consumer-build side effects or downstream processing.

The owner-approved operational packet must define failure escalation,
sanitized runner diagnostics, independent downstream health/result evidence,
retry/idempotency and recovery decisions, and an approved evidence store/access/
retention policy. The script's echoed response and HTTP marker are not a
monitoring system or acceptance gate. Keep SBOMs, tokens, customer metadata,
logs and deployment details out of public docs.

Operational runbooks remain with `Wardscan/ward-resources`; public product/
integration documentation remains with `Wardscan/ward-docs`. These are role
boundaries, not confirmed deployments or authority to change those repositories.

## This supplement's delivery status

Complete persistent documentation in an isolated worktree is the authorized
deliverable: **uncommitted, unpublished draft**. Independent review/adoption,
contract decisions, runtime verification, action publication, consumer rollout
and operations acceptance remain separate owner gates. No release evidence,
upload success, installed setting or activation is asserted. See the index's
proposed **UNPUBLISHED** shared lifecycle references, not an assumed live policy.
