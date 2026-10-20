# Changelog

All notable changes are recorded here. The format follows Keep a Changelog conventions.

## [Unreleased]

- Phase 19 validation is partially complete. A reproducible public npm workflow produced 85 package records, 10 declared
  funding sources, and 170 evidence records; GitHub API `403` responses and one npm metadata `404` remain explicit
  diagnostics. Independent user decision-impact evidence is still pending.
- Added `PHASE_19_VALIDATION.md` and the pinned `examples/phase-19-public-funding` input. A bounded version-specific npm
  metadata fix merged through fundgraph-core PR #12 as `93dc71ca25c4ab29594f5c43c01aed89063ac440` after successful
  CI; its publication remains pending the owner's interactive npm 2FA step.

- Completed Phase 17 release metadata and compatibility hardening. Published and publicly verified `@fundgraph/core@0.1.1` and `fundgraph@0.1.2`.
- Added canonical CLI npm metadata, an explicit executable mapping, a committed registry lockfile pinned to `@fundgraph/core@0.1.1`, and package metadata regression coverage.
- Verified CLI lint, typecheck, tests, build, package dry-run, cross-platform CI, package-artifact checks, and a clean Windows global install.
- Completed Phase 18 provider correctness and funding-evidence positioning. Added recorded npm, PyPI, and Cargo response tests for provenance, timestamps, raw payload retention, HTTPS declarations, and staleness semantics; narrowed project narratives and submission language around evidence rather than general dependency analysis.
- Resolved the restricted-Windows local cache-test limitation by using workspace-local test temporary directories and retaining atomic production cache replacement; the full core suite now passes 45 tests.

- Added end-to-end opt-in project analysis for npm, PyPI, and Cargo: dependency discovery now composes registry metadata, package funding declarations, GitHub `FUNDING.yml` evidence, relationship resolution, and deterministic reports through `--network`.
- Kept local/offline analysis as the CLI default and documented Go as discovery-only.
- Independent readiness audit completed on 2026-10-09; public repository state, remote CI, implementation claims, security controls, and release limitations are recorded in `AUDIT_REPORT.md`.
- Audit branch adds repository-level security policies and Dependabot configuration to `fundgraph-core` and `fundgraph-cli`.
- Audit remediation was merged through pull requests into all three `main` branches; the temporary audit branches were then removed after verification.
- Repository and documentation foundation established.
- Phase 1 core domain model, validation, deterministic serialization, error taxonomy, tests, and package baseline implemented.
- Phase 2 CLI foundation implemented with help/version commands, bounded JSON input, text/JSON output, offline/strict flags, exit codes, and CLI tests.
- Phase 3 dependency discovery implemented for npm, PyPI, and Cargo with workspaces, aliases, optional dependencies, transitive edges, lockfile diagnostics, fixtures, and CLI directory integration.
- Phase 4 ecosystem metadata adapters implemented for npm, PyPI, and Cargo with normalized package/repository identities, source evidence, timestamps, URL allowlists, payload limits, fixtures, and tests.
- Phase 5 funding evidence providers implemented for package metadata, GitHub FUNDING.yml, and recorded public provider responses with provenance, diagnostics, conflict preservation, fixtures, and tests.
- Phase 6 funding relationship resolution implemented with explicit rules, confidence levels, evidence links, ambiguity, contradiction, unresolved states, fixtures, and deterministic tests.
- Phase 7 deterministic reports implemented with a versioned machine-readable schema, text/JSON rendering, stable ordering, summaries, evidence drill-down, limitations, actions, diagnostics, fixtures, tests, and CLI integration.
- Phase 8 network reliability boundary implemented with typed failures, bounded retries, rate-limit backoff, opt-in TTL caching, cache invalidation, offline replay, cancellation, partial-result batches, and deterministic tests.
- Phase 9 security hardening completed with secure URL/redirect policy, SSRF-oriented destination checks, response/cache resource limits, authenticated-cache protection, adversarial fixtures, dependency audits, and documented residual risks.
- Phase 10 comprehensive fixture matrix and end-to-end integration coverage completed across npm, PyPI, Cargo, core report generation, malformed/failure categories, deterministic repeat runs, and CLI shared-fixture smoke tests.
- Phase 11 CI and packaging workflows completed for Ubuntu, Windows, and macOS on Node 20/22 with lint, typecheck, tests, builds, npm package checks, and artifact jobs.
- Phase 12 v0.1 product readiness completed with verified README/demo commands, release notes, final audit, local npm artifact installation checks, and documented publication limitations.
- Phase 13 external contributor readiness completed with issue/PR templates, adapter and fixture guidance, compatibility policy, good-first contribution guidance, and maintainer escalation/release runbooks.
- Phase 14 baseline Go module discovery added with deterministic `go.mod` parsing, malformed-input diagnostics, stable module-path identity, fixtures, tests, CLI integration, and explicit re-scoping of Go metadata/funding/workspace features.
- Pre-publication readiness completed with a corrected final audit, funding submission brief, publishing handoff, current artifact installation verification, and explicit external-publication boundaries.
- Published `@fundgraph/core@0.1.0` and `fundgraph@0.1.1` to npm. Verified a clean Windows global installation and merged the CLI executable fix through PR #9.
- Phase 16 post-release validation completed with deterministic published-CLI fixture analysis, representative offline repository checks, package compatibility verification, and a documented release-polish finding record.

## [0.1.0] - Published package baseline

- Core library package published as `@fundgraph/core@0.1.0`.
- CLI package baseline published as `fundgraph@0.1.0`; the corrected Windows executable is published as `fundgraph@0.1.1`.
