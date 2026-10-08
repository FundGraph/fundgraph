# Decision log

## D-0001 — Standalone repository

Date: 2026-10-08. FundGraph lives in `C:\Users\user\Projects\FundGraph` as one repository and will later map to `GITHUB_REPO=fundgraph`. No GitHub organization or remote is created by this project.

## D-0002 — Local-first, evidence-first scope

Date: 2026-10-08. v0.1 analyzes local dependency inputs and optional public metadata. It produces findings, not payments. This makes the tool useful without credentials and keeps the trust boundary explicit.

## D-0003 — Initial ecosystems

Date: 2026-10-08. The working v0.1 target is npm, PyPI, and Cargo. This choice provides meaningful coverage while keeping parser and fixture depth feasible; Phase 1 may re-scope it with evidence.

## D-0004 — No identity inference

Date: 2026-10-08. FundGraph reports package, repository, organization, and endpoint identifiers from sources. It does not assert that a person is a maintainer merely because their name appears in metadata.

## D-0005 — Three-repository architecture

Date: 2026-10-08. FundGraph is a multi-repository project consisting of three independent repositories contained within the `FundGraph` workspace:

1. `fundgraph` owns project-level governance, roadmap, cross-repository architecture, release coordination, and integration examples/fixtures.
2. `fundgraph-core` owns the reusable TypeScript domain model, dependency/evidence logic, adapters, report model, and library tests. It publishes the reusable package.
3. `fundgraph-cli` owns the executable `fundgraph` command, CLI UX, exit codes, CLI tests, and packaging of the executable. It depends on a versioned `fundgraph-core` package.

The split is not a monorepo: each repository has its own `.git`, history, branch, README, and release boundary. The parent workspace has no `.git`. Project-level documents are owned by `fundgraph`; repository-specific usage and development documentation is owned by the relevant implementation repository.

## D-0006 — Phase 1 model contract

Date: 2026-10-08. `fundgraph-core` uses schema version `1.0` and requires stable IDs on all domain entities, including `Confidence`. Validation rejects unsupported versions, unsafe URLs, oversized values, and malformed models. Contradictory relationships remain explicit through `status: contradictory` and `confidence.level: unknown`; they are never merged into a positive claim.

## D-0007 — Phase 2 input boundary

Date: 2026-10-08. The Phase 2 CLI accepts a JSON model document from a bounded file or stdin and delegates validation to `fundgraph-core`. It does not inspect manifests, perform dependency discovery, or access the network. This keeps the command contract testable while reserving ecosystem input handling for Phase 3.

## D-0008 — Phase 3 discovery boundary

Date: 2026-10-08. Phase 3 supports local npm, PyPI, and Cargo dependency discovery only. Lockfiles provide resolved versions and transitive edges when valid; missing or malformed lockfiles produce diagnostics rather than guessed versions. Registry metadata, repository normalization, and funding evidence remain separate adapter phases.

