## Task, scope and authority

- Canonical issue (`Refs`, not automatic closure) / approved spec revision:
- Repo / base and head SHA / allowed paths / non-goals:
- Accountable owner / writer / independent human reviewer:
- Acceptance cases / dependencies / unknowns with unblock owner and next action:
- Authorized stage and data, execution and publication boundaries:

## Action and consumer compatibility

- [ ] Diff stays within the approved scope; inherited/user work is preserved.
- [ ] Actual `action.yml` inputs, optional branches, absent/changed outputs,
      working directory and `sbom.json` behavior agree with docs and consumers.
- [ ] Consumer checkout/build/test evidence is separate from action scan/upload
      evidence; embedded build branches are not assumed absent.
- [ ] Runner OS/tools, installer/scanner versions, immutable action/dependency
      refs, registry access and downstream format/version decisions are recorded
      or explicitly unknown.
- [ ] Trusted workflow vs untrusted PR/source, secret/token permissions,
      expression-to-shell/JSON boundaries and response/SBOM logging are reviewed.
- [ ] Authentication, HTTP/transport failure, unsupported inputs, missing PR
      metadata and upload/processing acceptance are covered or owned deferrals.

## Verification and documentation

- Performed checks (exact commands/checks, revisions, environment and results):
- Skipped/unrun checks and reasons (including build/test/scan/upload):
- Docs/contract updates / sanitized evidence references / limitations:
- [ ] New/untracked files were read; local links, scoped globs and allowed paths
      were checked. No fabricated passing runtime or enforcement claims.
- [ ] HTTP 2xx/upload, scanner output, build, tests and deployment are reported
      as different evidence, not interchangeable success.

## Independent review and separate delivery gates

- Reviewer/date/decision / resolved findings / approved deferrals and owners:
- Action release/artifact/ref / consumer adoption / acceptance / rollback plan:
- Publication or execution approval / approved evidence store and retention:
- [ ] Review or merge does not authorize publishing a release, moving a ref,
      changing jobs/settings, using credentials, scanning or deployment.
- [ ] Shared policy references remain proposed/unpublished; supplemental docs
      are not implementation of the separate future CI task.
