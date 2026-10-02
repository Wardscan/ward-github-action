# Component overview

[Index](README.md) | [Contracts](contracts.md)

## Identity and provenance

Source: [action.yml](../action.yml) and [inherited README](../README.md) at
`5cbe4c668dd443bb6a761cde8b362c503f25ccb6`, static inspection on 2026-10-02.
The manifest names "Ward github action"; the README retains Mitigate branding
and earlier repository coordinates. Neither establishes migration compatibility.

This is a **composite action** (`runs.using: composite`) whose steps all declare
`shell: bash`. There is no declared JavaScript/Node action runtime, Docker action
image, module tree, separate executable entry point or action packaging build.
The manifest's inline commands are the executable surface.

## Source-to-upload path

| Boundary | Observed source behavior |
|---|---|
| Consumer workflow and checkout | Caller chooses events, runner, checkout/revision, working directory, credentials and registry login. The action contains no checkout step. |
| Dependency download | `Install Dependencies` fetches Syft's upstream `main` installer with curl and pipes it to `sh`, targeting `/usr/local/bin`. |
| Conditional consumer commands | `Build Gradle Jar`, `Build Maven Jar`, and `Install Node.js Dependencies` invoke caller-provided build/Sonar tooling for matching `type` values. |
| Scan | `Generate sbom` scans a registry image for `image`, otherwise the current directory; both write `sbom.json` using Syft's `cyclonedx-json` output selector. |
| Authentication and upload | `Asset sync` requests a client-credentials token and attempts a multipart asset sync using hardcoded remote destinations in the manifest. Endpoint strings are not duplicated here. |
| Reporting/artifacts | Upload response plus an HTTP-status marker is printed. No declared outputs, artifact-publication step, cleanup or downstream acceptance check exists. |

## Dependency and responsibility boundaries

Bash, POSIX `sh`, curl, grep, awk, filesystem write permissions and installer
access are prerequisites. Syft is installed at runtime without a pinned version
or checksum in this repository. Gradle wrapper/JDK, Maven/JDK, Node/npm and
Sonar configuration belong to the consumer's selected branch/tooling; no version
matrix or provisioning of those runtimes is defined here.

The README's consumer snippets use `ubuntu-latest`, checkout and, for image
scanning, a separate registry-login action. They are not a tested supported-OS
declaration. The source's Bash and `/usr/local/bin` assumptions require explicit
runner validation; Windows, macOS, non-root or self-hosted compatibility is unknown.
No Docker CLI or container build is invoked by this action.

This component does not own a consumer's build definition, deployment, service
operations or server schema. The desired review boundary keeps consumer build
and test evidence separate from scan/upload evidence; the current embedded build
branches remain an observed exception, not a refactoring performed here.

No source checkout SHA is explicitly attached to the upload. PR actor/title
fields are not commit identity. Caller workflow evidence must bind checked-out
revision, action ref, tools, scan target and SBOM digest to any later acceptance
record. Do not infer that scan inputs match a release artifact.
