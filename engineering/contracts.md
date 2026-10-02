# Observed action and consumer contracts

[Index](README.md) | [Development](development.md) | [Delivery](delivery.md)

Source authority: [action.yml](../action.yml) at
`5cbe4c668dd443bb6a761cde8b362c503f25ccb6`. These are implementation
observations, not approved server/API specifications or tested compatibility.

## Inputs and dispatch

All six declared inputs have empty-string defaults.

| Input | Declared required | Observed use |
|---|---|---|
| `assetid` | Yes | Interpolated into the asset-sync request path; no explicit script validation |
| `type` | No | Exact `gradle`, `maven`, `npm` select consumer commands; exact `image` selects a registry scan; every other value scans the current directory |
| `registry` | No | Declared but not referenced by the steps |
| `imagename` | No | Used directly after Syft's `registry:` prefix for `image`; not combined with `registry` |
| `client_id` | Yes | Interpolated into the client-credentials request form |
| `client_secret` | Yes | Interpolated into that form; sensitive, not a public example value |

`required` is metadata, not evidence of validated non-empty values. There is no
script-level supported-mode validation: empty or unknown `type` also takes the
directory-scan branch. The `type` description lists image/repo/gradle/npm but
omits implemented `maven`. `projectKey`, `projectName`, `sonarUrl`, `sonarToken`
are referenced without being declared. Do not document them as supported inputs
or assume their values reach consumer commands successfully.

The README documents only image/repo, lacks required authentication inputs,
and uses earlier action repository coordinates with `@main`. Whether those
coordinates resolve to a compatible action is unverified. Existing examples
are preserved, not endorsed or silently corrected.

## Checkout, scan and artifacts

The action performs no checkout or registry login, declares no step
`working-directory`, and does not read a workspace/revision input. It operates
in the current step working directory (normally the caller workspace; the caller
must confirm setup). A repository scan can include generated files present at
that point, including results of embedded consumer commands. This is not proof
of a clean checkout, complete dependency inventory or reproducible release build.

Image scans use `syft registry:<imagename>`; no image build occurs. Mutable image
tags do not establish an immutable scanned digest. Owner-approved consumer
evidence must bind exact checkout revision or image digest to the scan.

Both branches write the fixed relative file `sbom.json` using
`cyclonedx-json=sbom.json`. There is no collision guard, explicit cleanup,
retention configuration, `upload-artifact` step, declared `outputs` mapping or
`GITHUB_OUTPUT` use. The file is a workspace side effect, not a named action
output. Format/schema version, size limits, supported package coverage,
server validation rules and storage/retention are not specified here.

## Authentication, upload and metadata

`Asset sync` reads `github.event.pull_request.user.login` and
`github.event.pull_request.title` into misleadingly named `COMMIT_AUTHOR` and
`COMMIT_MESSAGE` variables. These are PR actor/title, not commit author/message
or a source SHA. Non-PR events and missing metadata have no explicit fallback or
validation. Direct expression interpolation into shell and handmade JSON is
not an escaping or input-safety guarantee.

The token request uses form-encoded `grant_type=client_credentials`, `client_id`
and `client_secret` against a hardcoded destination. An `access_token` is
extracted using grep/awk without a JSON parser or explicit response validation.
The extracted `token` variable is used in the upload's Bearer authorization
header. This wiring is not evidence of valid credentials, successful token
extraction or accepted authorization; no real token was obtained or used.

The upload uses POST to a hardcoded asset-sync path, with multipart `file` from
`sbom.json` (application/json) and `commitInfos` containing author/message JSON
(application/json), plus an accept header. The exact endpoint remains indexed
by the source's `Asset sync` step, not reproduced in this public baseline.
Accepted server payloads, tenancy/asset authorization, processing semantics,
limits, retries and error schema need an approved consumer/server contract.

## Status, errors and compatibility

The upload curl command captures body and a literal `HTTP_STATUS:` marker using
`-w`, then echoes the captured response. It has no HTTP-failure flag or status
check, explicit success/failure output, retry/idempotency policy, response-schema
validation or subsequent processing poll. HTTP 4xx/5xx are not explicitly
converted into failure by this script; actual transport/shell exit behavior
depends on the runner and commands and has not been exercised.

The installer curl uses `-sSfL`; that differs from token/upload calls and does
not establish error handling for the full action. Build/scanner commands can
fail, but there is no repository-tested failure matrix. Printed responses may
contain sensitive data; masking and safe log content have not been demonstrated.

An HTTP 2xx would be upload-response evidence only, not proof of authenticated
asset association, accepted/completed processing, successful tests/build,
release delivery or deployment. This supplement reports no such response.

Action SHA/ref, scanner/installer versions, caller checkout and build-tool
versions, image digest, SBOM schema and downstream service compatibility must
be reviewed together. Neither mutable `main` nor inherited major-version
dependency refs is immutable evidence; moving refs, adding/changing inputs or
outputs, removing build branches, or changing error semantics requires explicit
compatibility and release approval.
