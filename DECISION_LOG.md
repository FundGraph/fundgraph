# Decision log

## D-0016 - Phase 11 CI and package boundaries

Date: 2026-10-08. Each implementation repository owns its CI workflow and package artifact. `fundgraph-core` uses a committed npm lockfile and `npm ci`. `fundgraph-cli` installs a checked-out sibling `fundgraph-core` repository in CI and locally until the core package is published; it does not vendor or duplicate core source. CI verifies but does not publish, tag, push, or create GitHub resources.

## D-0015 - Phase 10 fixture and integration boundary

Date: 2026-10-08. The Phase 10 fixture matrix is owned by `fundgraph-core/test/fixtures` and is executed by a cross-stage integration suite. Integration tests use fixed repository fixtures for deterministic output, while temporary copies remain reserved for tests that intentionally exercise malformed or mutable inputs. The CLI smoke suite may consume the core repository’s fixtures but does not duplicate them.

## D-0014 - Phase 9 secure network boundary

Date: 2026-10-08. Network requests default to public credential-free HTTPS, reject private/local destinations and redirects, and enforce response-size limits. HTTP, provider host access, and cache use require explicit caller configuration. Authenticated requests bypass caches entirely. DNS resolution is intentionally outside this pure library boundary; callers needing DNS-rebinding protection must use controlled allowlists and network policy.

## D-0013 - Phase 8 network reliability boundary

Date: 2026-10-08. Live JSON request reliability is centralized in `fundgraph-core/src/network` and is opt-in. The boundary owns bounded retries, `Retry-After` handling, timeout/cancellation, typed failures, filesystem cache TTL/invalidation, offline replay, and batch partial-result semantics. Parsers remain pure and receive injected responses. Cache writes reject authorization/cookie-bearing requests, use restrictive permissions and atomic replacement, and stale offline data is labeled with a diagnostic rather than silently treated as fresh.

## D-0012 - Phase 7 report contract

Date: 2026-10-08. Reports are versioned `FundGraphReport` documents owned by `fundgraph-core`. The report contains stable arrays for domain records, relationship status summaries, evidence records referenced by relationship IDs, diagnostics, explicit limitations, and informational review/inspect actions. Text rendering escapes terminal control characters; JSON rendering uses deterministic object-key serialization. Actions are never executed by the library or CLI.

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

## D-0009 — Phase 4 metadata boundary

Date: 2026-10-08. Phase 4 parsers consume recorded JSON payloads through an injected context rather than performing live network requests. They allow only HTTPS sources for the relevant public registry, retain the raw payload and observation timestamp as evidence, normalize repository URLs without inferring people, and emit diagnostics for malformed or incomplete metadata.

## D-0010 — Phase 5 funding evidence boundary

Date: 2026-10-08. Funding providers emit declared URLs plus immutable evidence, but do not verify ownership, infer human identity, execute payments, or silently merge contradictory declarations. Package metadata, GitHub `FUNDING.yml`, and public provider responses are separate evidence kinds. Live network orchestration remains outside these pure parsers and will require the later error, cache, and rate-limit phase.

## D-0011 — Phase 6 resolution rules

Date: 2026-10-08. Relationship resolution accepts explicit repository candidates and funding claims. A single usable package→repository candidate is supported; multiple candidates are ambiguous; missing candidates are unresolved; and candidates referencing absent repositories are contradictory. Multiple explicit funding sources for one repository remain ambiguous. The resolver never selects a source based only on provider name or infers a human maintainer.

## D-0017 - Phase 12 local release candidate

Date: 2026-10-08. Phase 12 is complete for the local release candidate. The README and demo are verified against the
current CLI behavior, core and CLI npm artifacts install in isolated projects, and limitations are stated explicitly.
GitHub organization/repository creation, remote CI execution, npm publication, signing, and pushing remain maintainer
actions outside this task; the release is therefore ready locally but not published.

## D-0018 - Phase 13 contributor readiness

Date: 2026-10-08. Contributor governance is project-level, while each independent repository owns its repository-specific
entry points. The project repository owns the adapter guide, compatibility policy, good-first contribution guidance, and
maintainer runbook. All three repositories receive issue/PR templates because they may later have independent GitHub
repositories. New adapters remain fixture-first, evidence-bearing, deterministic, and subject to compatibility/security
review before implementation.

## D-0019 - Phase 14 baseline Go discovery

Date: 2026-10-08. Phase 14 promotes baseline Go module discovery from the backlog. `fundgraph-core` parses local
`go.mod` module and `require` directives, preserves Go module-path identity, records requested/resolved versions and
source locators, and emits deterministic malformed-input diagnostics. It does not invoke the Go toolchain, fetch modules,
parse `go.work`, derive transitive Go edges, or claim Go registry/funding support. Those capabilities require separate
evidence, fixtures, and acceptance criteria.

