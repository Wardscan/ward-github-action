# Development and verification

[Index](README.md) | [Review](ai-review.md)

## Prerequisites observed in source

Source: [action.yml](../action.yml), baseline
`5cbe4c668dd443bb6a761cde8b362c503f25ccb6`. This repo has no package manifest,
lockfile, wrapper, test suite, lint configuration or tracked workflow. Do not
run `npm install`, Maven or Gradle here as if this were the consumer application.

| Path selected by consumer | Required tooling/access; versions are not specified here |
|---|---|
| All action invocations | Bash, `sh`, curl, grep, awk; writable working directory and `/usr/local/bin`; authorized installer/token/upload network access; declared inputs |
| `image` | Syft registry access to the exact `imagename`; caller arranges registry credentials. `registry` is not consumed by the script. |
| Other modes, including `repo` | Intended consumer checkout/files in the current step working directory; Syft directory scan |
| `gradle` | Consumer `gradlew`, Java/Gradle dependencies, working-directory setup and Sonar configuration |
| `maven` | Consumer Maven/JDK, dependency access and Sonar configuration |
| `npm` | Consumer Node/npm, package scripts/dependencies and Sonar configuration |

The declared configuration keys are `assetid`, `type`, `registry`, `imagename`,
`client_id`, `client_secret`. Additional references to `projectKey`,
`projectName`, `sonarUrl`, `sonarToken` are **undeclared** inputs, not an accepted
configuration interface. npm steps additionally set `SONAR_PROJECT_KEY`,
`SONAR_PROJECT_NAME`, `SONAR_HOST_URL`, `SONAR_TOKEN` from those references.
Use key names only in documentation; never supply or inspect secret values.

No OS support matrix, exact tool versions, scanner format version, test fixture,
private dependency inventory or approved downstream compatibility is established.
Ubuntu is shown only in inherited consumer examples. Permission to write
`/usr/local/bin` is an assumption to validate, not authorization to elevate.

## Future commands, not executed

These are commands already embedded in the manifest, **not instructions to run
them for this supplement**. Future execution requires a separately approved
isolated consumer fixture, trusted code, permissions and external-service plan.

| Source branch | Commands requiring separate approval |
|---|---|
| Dependency installation | curl-to-`sh` installer in `Install Dependencies` |
| Gradle | `chmod +x gradlew`, `./gradlew clean assemble`, `./gradlew sonar -x compileTestJava` with the source's Sonar properties |
| Maven | `mvn clean install sonar:sonar` with the source's Sonar properties |
| npm | `npm install`, `npm run sonar` |
| Image SBOM | `syft registry:<approved-image-reference> -o cyclonedx-json=sbom.json` |
| Directory SBOM | `syft . -o cyclonedx-json=sbom.json` |
| Asset sync | Token request and multipart upload in `Asset sync`; no live credential or endpoint example is needed here |

Gradle assembly is not test proof and the Sonar invocation excludes
`compileTestJava`. Maven's lifecycle may execute consumer tests unless consumer
configuration skips them, but only an actual report proves execution/results.
`npm run sonar` depends entirely on the consumer's script. Package installation,
wrappers and build scripts can execute checked-out code and access networks.

## Offline verification for this supplement

Read all changed/new Markdown files and the source without executing it. Check
relative links and anchors, entry-point coverage, instruction frontmatter and
globs against real repository paths, and factual assertions against the manifest.
Compare complete `action.yml` content to the base in Git's canonical form,
accounting for checkout line-ending conversion; compare inherited README content
while allowing only the additive engineering pointer.

Read-only Git aids are `git status --short --untracked-files=all`,
`git diff --check` and `git diff --name-status`. The latter two do not check new
untracked file contents; inspect and validate those directly as well. Keep any
validation scripts/reports in session artifacts, not new repository tooling.

No existing automated docs checker or renderer is present. Offline checks do not
establish GitHub Actions parsing/runner behavior, Markdown rendering, lint,
build, tests, installation, scanning, authentication, uploading or server
processing. All such execution is **UNRUN** in this documentation-only unit.
