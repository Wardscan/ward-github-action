---
applyTo: "action.yml"
---

# Composite action source review

Follow [AGENTS.md](../../AGENTS.md). This scope matches the actual manifest and
inline scripts; there is no separate action source tree.

For separately authorized implementation, review declared vs referenced inputs,
conditional build branches, Bash quoting/expression interpolation, working
directory, scanner target/output, authentication, multipart metadata and failure
signaling against [contracts](../../engineering/contracts.md). Preserve consumer
compatibility or obtain explicit approval for a change.

Keep consumer build/test validation distinct from scanning/upload. Treat
downloaded installers, checked-out build scripts, PR metadata, registry contents,
credentials and response logs as separate trust boundaries. Do not turn an HTTP
response or printed status into acceptance evidence. Do not invent outputs,
supported OS/tool versions, test fixtures or a package-manager toolchain.

This docs-only supplement permits reading, not changing or executing `action.yml`.
Record source-observed gaps rather than silently fixing or claiming them resolved.
