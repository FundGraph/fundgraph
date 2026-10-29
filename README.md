# FundGraph

<p align="center">
  <img src="assets/fundgraph-project-v1.svg" alt="FundGraph: follow dependencies to funding declarations, with evidence" width="100%">
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-56d6be?style=flat-square" alt="MIT license"></a>
  <img src="https://img.shields.io/badge/runtime-Node.js%2020%20%7C%2022-83a8ff?style=flat-square" alt="Node.js 20 and 22">
  <img src="https://img.shields.io/badge/status-v0.1%20published-56d6be?style=flat-square" alt="v0.1 packages published">
</p>

<p align="center"><strong>Trace dependency funding declarations to their evidence—and keep uncertainty visible.</strong></p>

FundGraph is a local-first CLI and TypeScript library for evidence-first dependency funding analysis. It follows a
project's dependencies to declared funding pathways and preserves the source claims, provenance, conflicts, and
uncertainty needed for human review. Dependency discovery is the input; funding evidence is the product focus.

> Current scope: the CLI discovers dependency graphs locally by default. With explicit `--network`, it orchestrates
> npm/PyPI/Cargo metadata and declared funding evidence into a deterministic report. Go remains discovery-only.

## Repository role

| Repository | Owns | Start here when you are… |
|---|---|---|
| [`fundgraph`](https://github.com/FundGraph/fundgraph) | Product definition, roadmap, governance, cross-repository docs, and release coordination | deciding scope or understanding the whole project |
| [`fundgraph-core`](https://github.com/FundGraph/fundgraph-core) | Models, dependency discovery, evidence parsers, resolution, reports, and library tests | changing library behavior or adding a fixture/provider |
| [`fundgraph-cli`](https://github.com/FundGraph/fundgraph-cli) | The `fundgraph` command, output, exit codes, packaging, and CLI tests | changing command behavior or terminal output |

These are three independent repositories in the `FundGraph` workspace. `fundgraph-cli` depends on the published
`@fundgraph/core` package. The workspace parent is not a Git repository.

## How it works

```mermaid
flowchart LR
  A[Local project files] --> B[Core dependency discovery]
  B --> C[Dependency graph]
  C --> D[CLI text or JSON report]
  E[Recorded registry and funding data] --> F[Core evidence parsers]
  F --> G[Relationship resolution]
  G --> H[Versioned report API]
```

The current command analyzes local inputs for npm, PyPI, Cargo, and baseline Go `go.mod` requirements. Add explicit
`--network` to orchestrate npm/PyPI/Cargo metadata and declared funding evidence into the report. Go metadata and
funding providers remain future scope.

## Try it locally

For normal use, install the published CLI package:

```sh
npm install -g fundgraph@0.1.2
fundgraph --version
fundgraph analyze ./my-project --format text --offline
```

For repository development, from the workspace containing all three repositories:

```sh
cd fundgraph-core
npm ci
npm run build

cd ../fundgraph-cli
npm install --ignore-scripts --no-save ../fundgraph-core
npm run build
node dist/main.js --help
node dist/main.js analyze ../fundgraph-core/test/fixtures/npm-workspace --format text --offline
node dist/main.js analyze ../fundgraph-core/test/fixtures/npm-workspace --format json --offline
node dist/main.js analyze ./my-project --format json --network
```

## Evidence and safety

- Funding URLs are declarations to review, not endorsements or verified payment destinations.
- Multiple or contradictory sources stay separate; ambiguous relationships are not silently guessed.
- The system does not infer human identity, move money, manage wallets, or execute payments.
- Project files are treated as data. Directory analysis is local by default; `--network` is the explicit public-metadata opt-in.
- Network helpers live in core and require explicit caller configuration; DNS isolation remains an operational responsibility.

## Documentation

Start with [`PROJECT_CONTEXT.md`](PROJECT_CONTEXT.md), [`PROJECT_STATE.md`](PROJECT_STATE.md), and [`ROADMAP.md`](ROADMAP.md).
The product contract is in [`docs/PROJECT_CHARTER.md`](docs/PROJECT_CHARTER.md) and [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md).
The local release status is in [`FINAL_AUDIT.md`](FINAL_AUDIT.md); the factual funding brief is in
[`FUNDING_SUBMISSION.md`](FUNDING_SUBMISSION.md).

Repository governance is linked from [`CONTRIBUTING.md`](CONTRIBUTING.md), [`SECURITY.md`](SECURITY.md),
[`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md), and [`CHANGELOG.md`](CHANGELOG.md). The repository-specific
development model is documented in [`docs/DEVELOPMENT_MODEL.md`](docs/DEVELOPMENT_MODEL.md).

## Contributing

Read [`CONTRIBUTING.md`](CONTRIBUTING.md) and [`docs/CONTRIBUTOR_GUIDE.md`](docs/CONTRIBUTOR_GUIDE.md). Use
[`docs/GOOD_FIRST_ISSUES.md`](docs/GOOD_FIRST_ISSUES.md) for starter work and [`docs/ADAPTER_GUIDE.md`](docs/ADAPTER_GUIDE.md)
for fixture-first core contributions. See [`PUBLISHING_HANDOFF.md`](PUBLISHING_HANDOFF.md) for the maintainer's final
GitHub release steps.

For repository descriptions and GitHub topic tags, use [`GITHUB_REPOSITORY_METADATA.md`](GITHUB_REPOSITORY_METADATA.md).
