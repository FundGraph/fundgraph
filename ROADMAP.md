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

## PHASE 5 — Funding Evidence Providers — COMPLETE

**Purpose:** collect declared funding sources. **Prerequisites:** Phase 4.

**Objectives:** parse package funding metadata, GitHub `FUNDING.yml`, and supported provider URLs/API responses where public and useful; retain per-source provenance.

**Tests:** funded, unfunded, multiple, contradictory, malformed, and provider-failure fixtures.

**Security:** public network only by default, URL validation, SSRF controls, rate-limit handling, no credential requirement.

**Implemented:** `fundgraph-core` now parses npm/PyPI/Cargo funding metadata, GitHub `FUNDING.yml`, and recorded public provider responses. Every emitted funding source points to evidence containing the source, timestamp, parser, and raw observed payload. Multiple declarations remain separate; malformed files, unsafe URLs, oversized payloads, unfunded packages, and provider failures are explicit. **Acceptance/exit:** every emitted funding source points to one or more evidence records and no conflict is silently discarded. Verified with `npm test` in core (16 passing tests). **Artifacts:** `fundgraph-core/src/funding`, funding fixtures, and funding tests. **Next:** Phase 6.

## PHASE 6 — Funding Relationship Resolution — COMPLETE

**Purpose:** connect package → repository → funding source without overclaiming identity. **Prerequisites:** Phase 5.

**Objectives:** implement explicit resolution rules, confidence levels, conflict markers, and unresolved states; distinguish declared, corroborated, and ambiguous relationships.

**Tests:** positive, missing repository, conflicting repository, conflicting funding, and ambiguous mapping fixtures.

**Security:** no human identity inference; no authority based solely on a provider name.

**Implemented:** `fundgraph-core` now resolves explicit package→repository and repository→funding claims. It emits versioned relationships with rule IDs, evidence IDs, confidence, and supported/ambiguous/contradictory/unresolved status. Direct compatible evidence is high or medium confidence; missing identities are unresolved; multiple repository candidates and multiple funding claims remain ambiguous; missing referenced entities are contradictory. **Acceptance/exit:** relationship decisions are explainable from evidence and stable across runs. Verified with `npm test` in core (22 passing tests). **Artifacts:** `fundgraph-core/src/resolution`, resolver tests, and updated public API. **Next:** Phase 7.

## PHASE 7 — Deterministic Reports — COMPLETE

**Purpose:** make findings useful to humans and automation. **Prerequisites:** Phase 6.

**Objectives:** implement text, JSON, and machine-readable schema reports; stable sorting; summaries; evidence drill-down; explicit limitations and action links.

**Tests:** golden reports, ordering, empty graph, conflicts, network failures.

**Security:** escape terminal and structured output; never render metadata as executable markup.

**Implemented:** `fundgraph-core/src/reporting` now creates a versioned `FundGraphReport`, sorts all report collections deterministically, computes relationship status summaries, preserves diagnostics and contradictory states, exposes evidence references with source drill-down, and emits explicit limitations and review/inspect actions. Text output escapes control characters; JSON uses stable serialization. `fundgraph-cli` includes the report document in JSON output and renders the deterministic report after its compatibility summary. **Acceptance/exit:** same inputs and fixture data produce identical reports; verified with 25 core tests, 5 CLI tests, and TypeScript typechecks. **Artifacts:** reporting API, reporting fixtures/tests, and CLI integration. **Next:** Phase 8.

## PHASE 8 — Error Handling + Caching + Rate Limits — COMPLETE

**Purpose:** make network-assisted analysis reliable. **Prerequisites:** Phase 7.

**Objectives:** typed errors, bounded retries, opt-in cache, TTL/invalidation policy, offline replay, rate-limit backoff, partial-result semantics.

**Tests:** network failure, timeout, 429, corrupt cache, stale cache, cancellation.

**Security:** cache redaction and permissions; do not persist credentials or private source.

**Implemented:** `fundgraph-core/src/network` provides typed `FundGraphError` codes for network failures, timeouts, rate limits, cancellation, and cache faults. `NetworkClient` uses injected fetch/sleep/clock dependencies, bounded retries, capped exponential backoff, `Retry-After` handling, request timeouts, external cancellation, and non-retryable HTTP handling. Caching is opt-in, filesystem-backed, written with restrictive permissions and atomic replacement, keyed by URL hash, bounded by TTL, refreshed online, invalidated explicitly, and replayable offline with stale diagnostics. Authenticated requests are rejected for caching. `jsonBatch` preserves successful results and reports failures separately. **Acceptance/exit:** failures are actionable and do not erase successful partial evidence; verified with 31 core tests and 5 CLI tests. **Next:** Phase 9.

## PHASE 9 — Security Hardening — COMPLETE

**Purpose:** audit the trust boundary. **Prerequisites:** Phase 8.

**Objectives:** threat review, dependency audit, URL/redirect policy, resource limits, log review, malicious fixture suite, secure defaults.

**Tests:** adversarial inputs and regression tests.

**Implemented:** the Phase 9 audit is recorded in `SECURITY_AUDIT.md`. `fundgraph-core/src/network` now rejects private/loopback/local destinations, credential-bearing URLs, and redirects by default; supports explicit host allowlists; bounds response and cache sizes; bypasses cache reads and writes for authenticated requests; and preserves secure timeout, retry, and cancellation controls. Adversarial tests cover unsafe URLs, allowlists, redirects, oversized responses, credential leakage, and cache bypass. `npm audit --omit=dev --package-lock=false` reports zero vulnerabilities in both implementation repositories. **Acceptance/exit:** findings are documented, high-risk issues are fixed, and residual DNS/operational risks are explicitly accepted. Verified with 35 core tests, 5 CLI tests, typechecks, and package audits. **Next:** Phase 10.

## PHASE 10 — Comprehensive Fixtures + Integration Tests — COMPLETE

**Purpose:** validate end-to-end behavior. **Prerequisites:** Phase 9.

**Objectives:** complete fixture matrix; integration tests across all ecosystems; CLI smoke tests; coverage review.

**Implemented:** `fundgraph-core/test/fixtures/integration/fixture-matrix.json` identifies every required fixture category and physical fixture. `test/integration.test.js` executes discovery, metadata normalization, funding evidence parsing, relationship resolution, and report creation for npm, PyPI, and Cargo, then repeats the pipeline to verify deterministic output. It also verifies unfunded, multi-source, contradictory, missing-repository, and malformed-lockfile behavior. `fundgraph-cli` adds a smoke test against the shared npm workspace fixture and verifies report output. **Acceptance/exit:** required fixture categories pass and failures are diagnosable; verified with 38 core tests and 6 CLI tests. **Next:** Phase 11.

## PHASE 11 — CI + Cross-Platform Packaging — COMPLETE

**Purpose:** make the project reproducible for contributors and users. **Prerequisites:** Phase 10.

**Objectives:** CI for lint/typecheck/test/build; supported Node versions; npm packaging; Windows/macOS/Linux verification; provenance and release artifacts.

**Implemented:** both implementation repositories now contain GitHub Actions workflows covering Ubuntu, Windows, and macOS on Node 20 and Node 22. Workflows run lint, typecheck, tests, builds, package dry-runs, and artifact packaging with read-only permissions. `fundgraph-core` uses its committed lockfile with `npm ci`; `fundgraph-cli` checks out and installs the independently versioned sibling core repository before verification. Local sibling installation was verified on Windows. **Acceptance/exit:** clean-checkout workflows are defined, package installation works through the documented sibling-core path, and package artifacts are reproducible; verified with local lint/typecheck/test/build/package commands in both repositories. **Next:** Phase 12.

## PHASE 12 — v0.1 Product Readiness — COMPLETE

**Purpose:** release a credible, narrow product. **Prerequisites:** Phase 11.

**Objectives:** complete README demo; verify docs commands; remove placeholders; update changelog; prepare release notes; run final audit; document limitations and funding positioning.

**Implemented:** the project README and demo use the current CLI contract; stale Phase 2 wording and fictional output were removed; release notes and `FINAL_AUDIT.md` record the verified package baseline, limitations, security posture, and maintainer-owned release governance. Core and CLI package tarballs were installed in isolated temporary projects, npm packages were published, and a clean Windows global CLI installation was verified. **Acceptance/exit:** `FINAL_AUDIT.md` is honest, release artifacts are installable, the published package versions are recorded, and no unverified product claims remain. **Artifacts:** `RELEASE_NOTES_v0.1.0.md`, `FINAL_AUDIT.md`, updated README/demo/checklist, and verified npm artifacts. **Next:** Phase 13.

## PHASE 13 — External Contributor Readiness — COMPLETE

**Purpose:** make outside contribution safe and efficient. **Prerequisites:** Phase 12.

**Objectives:** issue templates, governance escalation, good-first issues, adapter guide, compatibility policy, maintainer runbook.

**Implemented:** project and repository contribution entry points now include issue forms, pull-request checklists,
good-first contribution shapes, adapter/fixture guidance, compatibility policy, and maintainer escalation/release
runbooks. The adapter guide identifies the owning source directories, fixture matrix, required evidence, security rules,
and exact verification commands. Core and CLI contributor guides preserve the three-repository dependency direction.
**Acceptance/exit:** a new contributor can identify the owning repository, run the documented checks, and add a recorded
fixture or provider using the documented workflow. Verified with 38 core tests, 6 CLI tests, lint/typecheck/build checks,
and documentation/link/template inspection. **Artifacts:** issue/PR templates in all repositories, `docs/ADAPTER_GUIDE.md`,
`docs/COMPATIBILITY_POLICY.md`, `docs/MAINTAINER_RUNBOOK.md`, `docs/GOOD_FIRST_ISSUES.md`, and repository contributor
guides. **Next:** Phase 14.

## PHASE 14 — v1 Expansion — COMPLETE

**Purpose:** expand only where evidence supports demand. **Prerequisites:** Phase 13 and usage feedback.

**Candidates:** Go modules, richer workspace support, more providers, offline registry snapshots, report integrations. Each candidate requires a new decision and acceptance criteria.

**Decision and scope:** baseline Go module discovery was promoted from the backlog because it extends the existing input boundary with a deterministic, local-only parser and a useful fourth ecosystem. The slice supports `go.mod` module and `require` directives, block and single-line requirements, indirect requirements, bounded input, malformed-manifest diagnostics, stable module-path identity, and CLI directory integration. It deliberately does not invoke Go, fetch modules, parse `go.work`, resolve transitive Go graph edges, normalize Go registry metadata, or collect Go funding evidence. Those remain future candidates and are not implied by this phase.

**Acceptance/exit:** a Go project with a valid `go.mod` produces deterministic dependency nodes with requested/resolved versions and source locators; malformed or oversized input produces diagnostics without guessed dependencies; existing ecosystem behavior remains unchanged; CLI integration continues to pass; and the scope/limitations are documented. Verified with the Go fixture and malformed-input tests, 40 core tests, 6 CLI tests, lint, typecheck, and builds. **Artifacts:** `fundgraph-core/src/inputs/go.ts`, `test/fixtures/go-module/go.mod`, discovery tests, updated fixture matrix, and compatibility/architecture/CLI documentation. **Next:** Phase 15 end-to-end orchestration.

**Skip/re-scope:** skip any expansion without maintainer or user evidence; preserve v0.1 simplicity. Future Go metadata, funding, and workspace work is explicitly re-scoped rather than assumed complete.

## PHASE 15 — End-to-End Funding Analysis Orchestration — COMPLETE

**Purpose:** make the implemented core stages usable as one product workflow for arbitrary supported projects. **Prerequisites:** Phases 1–14.

**Implemented:** `fundgraph-core` now exposes `analyzeProject`, which composes local dependency discovery, allowlisted npm/PyPI/Cargo registry metadata retrieval, package funding metadata parsing, evidence collection, relationship resolution, and deterministic report creation. `fundgraph-cli analyze --network` invokes this pipeline explicitly; default directory analysis remains local-only. Go remains discovery-only because Go metadata and funding providers are not implemented.

**Security:** network access is opt-in and uses the existing bounded `NetworkClient`; registry hosts are allowlisted, responses are bounded, cache/offline controls remain available to library callers, and reports never endorse or execute funding actions.

**Tests and acceptance:** the orchestration regression test uses a mocked registry response and verifies package, funding-source, evidence, and supported relationship output. Core passes 41 tests, lint, typecheck, build, and package dry-run. CLI passes 6 tests, lint, typecheck, and build. The CLI help and documentation expose the explicit `--network` contract.

**Artifacts:** `fundgraph-core/src/analysis.ts`, `fundgraph-core/test/analysis.test.js`, exported core API, CLI network option, updated CLI/project documentation. **Next:** Phase 16.

**Skip/re-scope:** do not add Go metadata/funding, automatic provider endorsement, payments, or hidden network access without a separately documented decision and acceptance criteria.

## PHASE 16 — Post-release Validation and Submission Readiness — COMPLETE

**Purpose:** validate the first public npm package workflow with reproducible usage evidence before expanding product scope.

**Why it exists:** publication is complete, but publication alone does not establish adoption, reliability across representative projects, or funding-program eligibility. This phase turns real usage feedback into evidence and a justified next engineering decision without inventing traction.

**Prerequisites:** Phase 15 complete; `@fundgraph/core@0.1.0` and `fundgraph@0.1.1` published; CLI Windows installation verified; no unresolved release-blocking CI failures.

**Objectives:**

- Run documented clean-install and smoke-analysis workflows against selected public or owner-controlled projects without uploading private source.
- Record reproducible usability findings, unsupported inputs, network failures, and report-quality issues.
- Verify package/version compatibility and update release, security, and limitation records when facts change.
- Prepare factual Drips/GrantFox submission material without claiming adoption, eligibility, acceptance, or maintainer identity.
- Select exactly one next product expansion only after evidence supports it: non-GitHub funding-file orchestration, complete Go metadata/funding, CLI report usability, or offline registry snapshots.

**Expected files/components:** project `PROJECT_STATE.md`, `FINAL_AUDIT.md`, `FUNDING_SUBMISSION.md`, `CHANGELOG.md`, release notes, compatibility records, and (only if required by verified findings) core/CLI tests and implementation files.

**Implementation tasks:**

1. Reproduce global installation for the published versions and record the exact commands and results.
2. Analyze representative projects in offline mode; use `--network` only for public metadata and only with explicit review.
3. Record findings as documentation-backed evidence; do not create contributor issues during this phase unless separately authorized.
4. Review package metadata, repository links, security policy, and supported-version statements.
5. Derive and document the next phase from observed evidence and the existing backlog.

**Tests required:** clean npm installation, CLI version/help, offline fixture analysis, deterministic repeated output, representative-project smoke tests, core/CLI lint/typecheck/test/build, and package metadata verification. Any network or registry failure must be recorded as blocked/inconclusive rather than passed.

**Documentation required:** update project state, changelog, final audit, funding brief, release notes, and decision log with verified results and remaining limitations.

**Security considerations:** never send private project files to external services; keep network access opt-in; preserve URL allowlists, response bounds, cache rules, and evidence uncertainty; do not treat funding URLs or usage results as endorsements.

**Acceptance criteria:** published packages install from a clean environment; documented commands work; at least one representative analysis is reproducible; any failures are classified; submission materials contain only verified facts; no new scope is selected without evidence.

**Exit criteria:** results are recorded, documentation matches observed behavior, package compatibility is confirmed, and a single evidence-backed Phase 17 proposal is documented before implementation.

**Expected artifacts:** validation record, updated final audit/release records, factual funding submission package, and a Phase 17 decision entry.

**Immediately after:** define Phase 17 from observed demand and implement only its approved acceptance criteria.

**Skip/re-scope:** skip expansion work if no representative usage evidence exists; re-scope to release correction if package installation, CLI behavior, security, or documentation defects are found.

**Completed:** published package installation, registry visibility, CLI help/version, deterministic fixture analysis, representative offline repository analysis, package compatibility review, submission-material review, and implementation verification were completed. The validation record is [`PHASE_16_VALIDATION.md`](PHASE_16_VALIDATION.md). The CLI repository's missing-lockfile partial result and npm repository-metadata omissions are recorded as remaining P1 release-polish findings. No contributor issues or ecosystem expansion were created.

## PHASE 17 — Release Metadata and Compatibility Hardening — COMPLETE

**Purpose:** address the concrete Phase 16 release-quality findings before selecting a new ecosystem or funding provider.

**Why it exists:** published packages work, but npm repository metadata is absent and the CLI has no committed lockfile. These issues affect discoverability and reproducibility more directly than speculative feature expansion.

**Prerequisites:** Phase 16 complete; owner approval for any new npm patch publication or lockfile policy change; no need to create contributor issues.

**Objectives:** decide and document the CLI lockfile strategy; add verified repository metadata to future package manifests; define a cross-repository compatibility matrix; collect real maintainer/user feedback when available; keep funding claims and adoption statements factual.

**Expected files/components:** `fundgraph-core/package.json`, `fundgraph-cli/package.json`, lockfile policy/compatibility documentation, release notes, and package metadata tests. New package versions or publication are owner-controlled actions.

**Tests required:** package metadata assertions, clean-install tests, core/CLI compatibility checks, lint/typecheck/test/build/package dry-runs, and a repeated CLI smoke analysis.

**Security considerations:** repository URLs must be verified before publication; lockfiles must not contain credentials or private registry data; no private source may be sent to external services.

**Acceptance criteria:** the lockfile decision is explicit; verified repository metadata is present in the next package release or intentionally deferred with rationale; compatible core/CLI versions are documented; no unsupported ecosystem/provider is added.

**Exit criteria:** release-polish findings are resolved or explicitly accepted, and only then is a demand-backed feature phase proposed.

**Skip/re-scope:** if package metadata and reproducibility are acceptable to the owner, skip implementation and record the decision; if real usage identifies a more urgent correctness defect, re-scope to that defect with regression coverage.

**Completed:** `@fundgraph/core@0.1.1` and `fundgraph@0.1.2` were published and verified in the public npm registry. The CLI gained canonical npm discoverability metadata, an explicit `fundgraph` executable mapping, a committed registry lockfile pinned to `@fundgraph/core@0.1.1`, and package metadata regression tests. PR #10 merged the CLI changes through the normal GitHub path as `ed3e2e02d9b2666f4400c751c8aab7089d4d92e5`. Local validation, cross-platform CI, package-artifact checks, public npm metadata checks, and a clean Windows global install all passed. Detailed evidence is in [`PHASE_17_VALIDATION.md`](PHASE_17_VALIDATION.md). No contributor issues or ecosystem expansion were created.

**Next:** Phase 18 must be derived from real usage feedback and documented before implementation. Candidate directions remain non-GitHub funding-file orchestration, complete Go metadata/funding support, improved CLI report usability, or offline registry snapshots, but none is approved until demand and acceptance criteria are recorded.

## PHASE 18 — Provider Correctness and Funding-Evidence Positioning — COMPLETE

**Purpose:** strengthen correctness around recorded provider observations and make the public product narrative accurately center funding evidence.

**Objectives:** add deterministic npm/PyPI/Cargo provider fixtures and regression tests; preserve provenance and observation timestamps; document staleness and refresh expectations; update project, core, and CLI narratives and submission language; retain explicit non-goals.

**Completed:** provider correctness tests were added and merged in `fundgraph-core` PR #10 (`c9f3da0`). They verify recorded registry provenance, parser identity, raw payload preservation, timestamps, HTTPS declarations, and point-in-time snapshot semantics. The project evidence model, core README, CLI README, project README, context, and funding submission brief now make funding evidence the product focus and clearly describe staleness. The versioned public packages remain `@fundgraph/core@0.1.1` and `fundgraph@0.1.2`; no artificial version bump was created for documentation-only changes. CLI narrative changes merged in PR #11 (`a54b25d`).

**Validation:** core provider tests pass in the normal cross-platform CI matrix and package-artifact jobs. A follow-up cache-test harness fix merged in `fundgraph-core` PR #11 (`8a2cbe6`) makes the full local Windows suite pass by using workspace-local temporary directories; production cache writes retain atomic replacement. CLI CI and package-artifact checks pass.

**Exit criteria:** complete. No new ecosystem, provider, payment capability, contributor issue, or funding claim was introduced.

**Next:** derive Phase 19 from real usage feedback. Do not add ecosystems speculatively.

## PHASE 19+ — Long-Term Development

**Purpose:** derive each later phase from the mission, requirements, architecture, backlog, verified usage evidence, ecosystem changes, and user needs. **Rule:** document the proposed phase in this roadmap before implementation. Never treat the end of this list as the end of the project.

