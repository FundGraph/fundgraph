# Compatibility policy

## Scope

FundGraph has three independently versioned repositories. The project-level `fundgraph` repository coordinates policy;
`fundgraph-core` owns the reusable API and schema; `fundgraph-cli` owns the executable interface.

## Supported baseline

- Node.js 20 and 22 are the supported runtime versions for v0.1.
- Windows, macOS, and Linux are covered by the repository CI definitions.
- v0.1 ecosystems are npm, PyPI, and Cargo.
- Core schema version `1.0` and the published `@fundgraph/core` package version `0.1.x` are the compatibility baseline.

## Change rules

- Patch releases fix defects without intentionally changing public model meaning or CLI exit codes.
- Minor releases may add fields, diagnostics, providers, or commands while preserving existing valid inputs and output
  contracts where practical.
- Major releases may remove or change public APIs, schema semantics, supported runtimes, or CLI behavior and require
  migration notes.
- Any change to evidence semantics, relationship status, confidence, URL policy, or report schema requires a decision
  log entry and regression fixtures.

## Cross-repository order

When an API change is necessary, update and test `fundgraph-core` first. Release a compatible core version before changing
`fundgraph-cli` to consume it. The CLI must not copy core logic. Project-level documentation and release notes record the
compatible versions and coordinated release status.

Unsupported environments may still run, but maintainers do not promise identical behavior outside the tested Node and OS
matrix. Compatibility claims must be supported by CI or an explicitly documented local verification.
