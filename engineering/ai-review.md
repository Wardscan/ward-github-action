# AI-assisted review and acceptance

[Index](README.md) | [Agent policy](../AGENTS.md) |
[PR packet](../.github/pull_request_template.md)

## Review authority

Use the approved task packet, exact action/consumer revisions and
[observed contract](contracts.md), not generic service rules or legacy README
examples as proof. An agent may prepare evidence/findings; an independent human
reviews and accepts them. No named reviewer, active required check or enforced
merge rule is established by these files.

The [shared WARD lifecycle](https://github.com/Maggioli-Greece/issues/blob/main/docs/ward-pilot/lifecycle.md)
is proposed **UNPUBLISHED**. Its requirements, Ready, implementation, review,
acceptance, release, operations and docs/evidence gates guide this draft but are
not activated settings. Shared private material must not be quoted into public
action documentation.

## Trust and permission checklist

- [ ] Distinguish trusted workflow/action ref from checked-out consumer content.
      Record event, checkout revision, working directory and which code is run.
      Never execute untrusted PR code with privileged credentials; a privileged
      event such as `pull_request_target` is not permission to check out and run
      PR build scripts. Do not assume fork secret availability.
- [ ] Review PR actor/title and action inputs before expression-to-shell/JSON
      use. Current interpolation has no demonstrated escaping/validation.
      Optional build branches execute consumer wrappers/scripts; package
      installation also executes code. A scan-only assumption is unsafe here.
- [ ] Use caller-owned least-privilege job/token permissions and separately
      approved client/registry credentials. The action declares no `permissions`,
      uses no explicit `GITHUB_TOKEN`, and does not arrange checkout or login;
      these facts do not prove that inherited job credentials are inaccessible
      to consumer scripts. Record checkout credential persistence decisions.
- [ ] Review installer network trust, mutable refs, `/usr/local/bin` write
      permissions, image access and scanner target. No action/download pin or
      runtime-version support matrix is established by this source.
- [ ] Treat working-tree contents, build products, SBOM/package metadata, PR
      metadata and asset identity as potentially restricted. Do not send
      private/customer data to unapproved services or public evidence stores.
- [ ] Keep tokens, credentials and raw responses out of public logs/docs. Review
      current response printing and credential form/header handling; repository
      documentation cannot prove GitHub masking or remote access control.

## Contract and acceptance checklist

- [ ] All six declared inputs, empty defaults, exact type dispatch, unused
      `registry`, undeclared Sonar references and missing input validation are
      understood. Do not invent server formats/versions/limits or a new API.
- [ ] Checkout/build identity, image digest or directory contents, Syft version/
      output schema and fixed `sbom.json` side effect are bound to evidence.
      No declared action output or revision attachment is assumed.
- [ ] Cases include empty/unknown type, missing image/credentials/workspace,
      failed download/build/scan/auth, HTTP rejection, missing PR metadata,
      payload encoding and downstream acceptance. They are future approved
      checks, **not executed tests** in this baseline.
- [ ] Token extraction and Bearer-header wiring are reviewed separately from
      credential validity and accepted authorization; no working or repaired
      integration is inferred from source alone.
- [ ] Transport/HTTP status, upload, server processing, consumer build/tests,
      action publication and deployment are separate evidence and decisions.
      HTTP 2xx is not acceptance proof.
- [ ] Legacy coordinates, mutable refs, tool compatibility and all contract/
      behavior changes have explicit consumer/release decisions.

## Stop, evidence and independent decision

Stop for missing owners/approvals, conflicting work, unsafe credentials/data,
unknown required contracts or incompatible consumer/release decisions. Record
the finding, unblock owner and next action; do not activate a workflow or silently
fix source while delivering a docs-only baseline. Repeated correction failures
require human escalation, not an unbounded agent run.

The review record identifies reviewer/date, exact source and document revisions,
performed offline checks, unrun runtime/build/test/scan/upload checks with reasons,
limitations, resolved findings and approved deferrals. Evidence access, storage
and retention require owner approval. Human adoption and publication remain
pending; merge, agent-authored policy or a response log does not complete the
lifecycle or authorize delivery/deployment.
