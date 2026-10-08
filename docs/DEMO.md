# Product demo

This demo shows the currently implemented CLI behavior: local dependency discovery and deterministic reporting. It does not
claim that the CLI currently performs a complete dependency-to-funding analysis.

## Run the local discovery demo

Build `fundgraph-core`, install it into `fundgraph-cli` using the local sibling-package instructions in the CLI README,
then run from the `fundgraph-cli` repository:

```sh
node dist/main.js analyze ../fundgraph-core/test/fixtures/npm-workspace --format text --offline
node dist/main.js analyze ../fundgraph-core/test/fixtures/npm-workspace --format json --offline
```

The output includes the analyzed input, discovered ecosystem, dependency/model counts, diagnostics, and the core report.
Counts come from the committed synthetic fixture and are not user or adoption metrics.

## What the demo establishes

- Project manifests and lockfiles are read locally as data.
- The dependency graph is passed to the core report builder.
- Text and JSON forms are available for human and tool consumption.
- The same fixture produces deterministic results.

## Evidence and funding functionality

The core library has separate APIs for recorded npm/PyPI/Cargo registry metadata, package funding declarations, GitHub
`FUNDING.yml`, relationship resolution, and evidence-backed reports. These APIs are exercised with recorded fixtures in
the core test suite. The current CLI directory command does not yet orchestrate those stages against arbitrary projects
or perform live provider requests.

Never present a declaration as verification of a maintainer's identity, an endorsement of a funding destination, or a
payment action. See [`FUNDING_SUBMISSION.md`](../FUNDING_SUBMISSION.md) for accurate product positioning.
