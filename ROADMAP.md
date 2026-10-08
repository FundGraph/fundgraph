# FundGraph roadmap

This is an executable roadmap. A phase is complete only when its acceptance and exit criteria are verified against the repository, tests, and documentation. If a phase is skipped or re-scoped, record why in `DECISION_LOG.md` and update `PROJECT_STATE.md`.

## Workspace architecture

FundGraph is a multi-repository project consisting of three independent repositories contained within the `FundGraph` workspace:

- `fundgraph`: project-level documentation, governance, roadmap, release coordination, examples, and integration fixtures.
- `fundgraph-core`: reusable and publishable library/domain package with parsers, evidence, resolution, reports, and library tests.
- `fundgraph-cli`: publishable executable package providing the `fundgraph` command and CLI-specific tests.

The dependency direction is `fundgraph-cli` → `fundgraph-core`. The project-level `fundgraph` repository coordinates both and must not become a fourth implementation package. The workspace directory itself must not contain `.git`.

## PHASE 0 — Repository + Documentation Foundation — COMPLETE

**Purpose:** establish the durable source of truth before implementation. **Why:** future agents and contributors need product, security, scope, and release context without relying on chat history. **Prerequisites:** none.

**Objectives and tasks:** create governance files; research adjacent tools; define v0.1 scope, architecture, data/evidence models, security, testing, contribution, release, and funding positioning; establish the three-repository architecture and documentation ownership; create state and roadmap records.

**Expected files:** root governance files and `docs/PROJECT_CHARTER.md`, `REQUIREMENTS.md`, `ARCHITECTURE.md`, `DATA_MODEL.md`, `EVIDENCE_MODEL.md`, `CLI_SPEC.md`, `SECURITY.md`, `COMPETITIVE_LANDSCAPE.md`, `TESTING.md`, `CONTRIBUTOR_GUIDE.md`, `RELEASE_PROCESS.md`, `DEVELOPMENT_MODEL.md`, `DEMO.md`.

**Tests:** repository and documentation consistency checks; no product implementation tests yet.

**Security:** no remote, credentials, private data, payment execution, or identity inference.

**Acceptance/exit:** all required project documents exist in `fundgraph`, scope is explicit, research is recorded, all three repositories have independent Git roots and README files, the workspace has no `.git`, state says complete, and Phase 1 is actionable. **Artifacts:** the three-repository workspace. **Next:** Phase 1. **Skip/re-scope:** only if an existing authoritative repository is discovered; preserve its history and document the migration.

## PHASE 1 — Architecture + Domain Model — COMPLETE

**Purpose:** turn the documented model into versioned TypeScript types and validation. **Why:** parsers and reporters need one stable contract. **Prerequisites:** Phase 0.

**Objectives:** create package/tooling baseline; define versioned `Project`, `Dependency`, `Package`, `Registry`, `Repository`, `FundingSource`, `Evidence`, `Relationship`, and `Confidence`; implement validation and stable serialization; define error taxonomy.

**Expected changes in `fundgraph-core`:** `package.json`, `tsconfig.json`, `src/domain`, `src/core`, schema tests, package README and repository-specific docs. Update project-level docs in `fundgraph` when contracts change.

**Tests:** valid/invalid model fixtures, schema compatibility, deterministic serialization, contradictory evidence representation.

**Security:** reject unsafe URLs and oversized/untrusted fields; avoid logging secrets.

**Implemented:** `fundgraph-core` now contains strict TypeScript models for all nine required entities, schema version `1.0`, model validation, deterministic serialization, typed errors, a small public API, and tests. **Acceptance/exit:** models validate, serialize deterministically, and are consumed by a small library API. Verified with `npm run typecheck`, `npm test` (4 passing tests), and `npm pack --dry-run`. **Artifacts:** `fundgraph-core/src`, `fundgraph-core/test`, generated package declarations/build output, and package metadata. **Next:** Phase 2. **Skip/re-scope:** if a simpler representation demonstrably preserves versioning and evidence semantics.

## PHASE 2 — CLI Foundation — COMPLETE

**Purpose:** provide a stable command surface. **Prerequisites:** Phase 1.

**Objectives:** implement `fundgraph analyze`, `fundgraph version`, and `fundgraph --help`; support input path, output format, offline mode, and strictness options; return meaningful exit codes.

**Tests:** help, version, invalid arguments, stdin/path behavior, JSON/text output contracts.

**Security:** no shell evaluation of input; bounded file reads; clear network opt-in.

**Implemented:** `fundgraph-cli` now provides `--help`, `version`, and `analyze`; accepts stdin or bounded JSON file input; supports text/JSON output, offline, and strict flags; invokes `@fundgraph/core` validation; and returns documented exit codes. **Acceptance/exit:** CLI invokes library validation without duplicating domain logic and passes help, version, stdin/path, format, invalid-argument, partial, and strict tests. Verified with `npm run typecheck` and `npm test` (4 passing tests). **Artifacts:** `fundgraph-cli/src`, `fundgraph-cli/test`, package/bin metadata, and repository README. **Next:** Phase 3. **Skip/re-scope:** never skip the stable command contract; reduce options if deadline pressure requires it.

## PHASE 3 — Dependency Discovery — COMPLETE

**Purpose:** discover direct/transitive dependencies from supported project inputs. **Prerequisites:** Phase 1–2.

**Objectives:** implement npm, PyPI, and Cargo manifest/lockfile discovery; handle aliases, workspaces, optional dependencies, malformed inputs, and missing lockfiles; preserve source locations.

**Tests:** deterministic fixtures for every listed case and dependency graph snapshots.

**Security:** treat manifests and lockfiles as hostile data; no code execution; path traversal protection; size limits.

**Implemented:** `fundgraph-core` now discovers npm, PyPI, and Cargo dependency graphs from local manifests and lockfiles. It handles npm aliases, npm/Cargo workspaces, optional dependencies, transitive lockfile edges, missing lockfiles, malformed lockfiles, bounded inputs, and source paths/locators. `fundgraph-cli analyze <directory>` delegates to this API. **Acceptance/exit:** supported fixtures produce correct graph nodes/edges and actionable diagnostics. Verified with `npm test` in core (8 passing tests) and CLI (5 passing tests). **Artifacts:** `fundgraph-core/src/inputs`, deterministic fixtures under `fundgraph-core/test/fixtures`, discovery tests, and CLI integration tests. **Next:** Phase 4. **Skip/re-scope:** an ecosystem may be deferred only with explicit fixture and user-value evidence.

## PHASE 4 — Initial Ecosystem Parsers — COMPLETE

**Purpose:** normalize package metadata and repository links across the selected ecosystems. **Prerequisites:** Phase 3.

**Objectives:** define registry adapters and normalized package/repository identity; keep source payloads and timestamps; tolerate malformed metadata.

**Tests:** recorded fixture responses, aliases, scoped names, alternate repository URL forms, missing metadata.

**Security:** allowlist hosts/methods; bound response size; never execute fetched content.

**Implemented:** `fundgraph-core` now normalizes recorded npm, PyPI, and Cargo registry payloads into versioned registry, package, and repository models. It retains raw payloads, source URLs, parser identifiers, and observation timestamps as evidence; canonicalizes repository URLs; tolerates missing/malformed fields; bounds payloads; and restricts metadata sources to HTTPS registry allowlists. **Acceptance/exit:** each v0.1 ecosystem has a parser with deterministic normalized output. Verified with `npm test` in core (11 passing tests), including recorded responses, scoped names, alternate repository URLs, missing metadata, unsafe sources, and oversized payloads. **Artifacts:** `fundgraph-core/src/metadata`, recorded metadata fixtures, and metadata tests. **Next:** Phase 5.

## PHASE 5 — Funding Evidence Providers

**Purpose:** collect declared funding sources. **Prerequisites:** Phase 4.

**Objectives:** parse package funding metadata, GitHub `FUNDING.yml`, and supported provider URLs/API responses where public and useful; retain per-source provenance.

**Tests:** funded, unfunded, multiple, contradictory, malformed, and provider-failure fixtures.

**Security:** public network only by default, URL validation, SSRF controls, rate-limit handling, no credential requirement.

**Acceptance/exit:** every emitted funding source points to one or more evidence records and no conflict is silently discarded. **Next:** Phase 6.

## PHASE 6 — Funding Relationship Resolution

**Purpose:** connect package → repository → funding source without overclaiming identity. **Prerequisites:** Phase 5.

**Objectives:** implement explicit resolution rules, confidence levels, conflict markers, and unresolved states; distinguish declared, corroborated, and ambiguous relationships.

**Tests:** positive, missing repository, conflicting repository, conflicting funding, and ambiguous mapping fixtures.

**Security:** no human identity inference; no authority based solely on a provider name.

**Acceptance/exit:** relationship decisions are explainable from evidence and stable across runs. **Next:** Phase 7.

## PHASE 7 — Deterministic Reports

**Purpose:** make findings useful to humans and automation. **Prerequisites:** Phase 6.

**Objectives:** implement text, JSON, and machine-readable schema reports; stable sorting; summaries; evidence drill-down; explicit limitations and action links.

**Tests:** golden reports, ordering, empty graph, conflicts, network failures.

**Security:** escape terminal and structured output; never render metadata as executable markup.

**Acceptance/exit:** same inputs and fixture data produce identical reports. **Next:** Phase 8.

## PHASE 8 — Error Handling + Caching + Rate Limits

**Purpose:** make network-assisted analysis reliable. **Prerequisites:** Phase 7.

**Objectives:** typed errors, bounded retries, opt-in cache, TTL/invalidation policy, offline replay, rate-limit backoff, partial-result semantics.

**Tests:** network failure, timeout, 429, corrupt cache, stale cache, cancellation.

**Security:** cache redaction and permissions; do not persist credentials or private source.

**Acceptance/exit:** failures are actionable and do not erase successful partial evidence. **Next:** Phase 9.

## PHASE 9 — Security Hardening

**Purpose:** audit the trust boundary. **Prerequisites:** Phase 8.

**Objectives:** threat review, dependency audit, URL/redirect policy, resource limits, log review, malicious fixture suite, secure defaults.

**Tests:** adversarial inputs and regression tests.

**Acceptance/exit:** findings are documented and high-risk issues are fixed or explicitly accepted. **Next:** Phase 10.

## PHASE 10 — Comprehensive Fixtures + Integration Tests

**Purpose:** validate end-to-end behavior. **Prerequisites:** Phase 9.

**Objectives:** complete fixture matrix; integration tests across all ecosystems; CLI smoke tests; coverage review.

**Acceptance/exit:** required fixture categories pass and failures are diagnosable. **Next:** Phase 11.

## PHASE 11 — CI + Cross-Platform Packaging

**Purpose:** make the project reproducible for contributors and users. **Prerequisites:** Phase 10.

**Objectives:** CI for lint/typecheck/test/build; supported Node versions; npm packaging; Windows/macOS/Linux verification; provenance and release artifacts.

**Acceptance/exit:** clean checkout passes and package installation works. **Next:** Phase 12.

## PHASE 12 — v0.1 Product Readiness

**Purpose:** release a credible, narrow product. **Prerequisites:** Phase 11.

**Objectives:** complete README demo; verify docs commands; remove placeholders; update changelog; prepare release notes; run final audit; document limitations and funding positioning.

**Acceptance/exit:** `FINAL_AUDIT.md` is honest, checklist passes, release artifact is installable, and no unverified claims remain. **Next:** Phase 13.

## PHASE 13 — External Contributor Readiness

**Purpose:** make outside contribution safe and efficient. **Prerequisites:** Phase 12.

**Objectives:** issue templates, governance escalation, good-first issues, adapter guide, compatibility policy, maintainer runbook.

**Acceptance/exit:** a new contributor can run tests and add a fixture/provider from docs. **Next:** Phase 14.

## PHASE 14 — v1 Expansion

**Purpose:** expand only where evidence supports demand. **Prerequisites:** Phase 13 and usage feedback.

**Candidates:** Go modules, richer workspace support, more providers, offline registry snapshots, report integrations. Each candidate requires a new decision and acceptance criteria.

**Skip/re-scope:** skip any expansion without maintainer or user evidence; preserve v0.1 simplicity.

## PHASE 15+ — Long-Term Development

**Purpose:** derive the next phase from the mission, requirements, architecture, backlog, issues, implementation state, ecosystem changes, and user needs. **Rule:** document the proposed phase in this roadmap before implementation. Never treat the end of this list as the end of the project.

