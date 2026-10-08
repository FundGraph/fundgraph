# Changelog

All notable changes are recorded here. The format follows Keep a Changelog conventions.

## [Unreleased]

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

## [0.1.0] - Unreleased

- Release candidate prepared locally; publication remains pending maintainer-created GitHub/npm resources.

