# Project state

```yaml
current_phase: 15
current_status: published-v0.1-release-with-post-publication-validation
last_completed_phase: 15
current_objective: Complete post-publication validation and prepare evidence-based Drips/GrantFox submission materials without overstating adoption or eligibility.
completed:
  - Phase 0 documentation and research foundation created
  - Project charter, requirements, architecture, data/evidence/security models documented
  - Focused ecosystem research recorded
  - Executable roadmap and governance documents created
  - Three-repository architecture designed and documented
  - Foundation history retained in the project-level fundgraph repository
  - Independent fundgraph-core and fundgraph-cli repositories initialized with package boundaries
  - Parent workspace verified as a container without .git
  - Phase 1 core package, versioned domain models, validation, deterministic serialization, and error taxonomy implemented
  - Phase 1 core tests and package dry-run verified
  - Phase 2 CLI command surface, input handling, output formats, exit codes, and tests implemented
  - Phase 3 npm, PyPI, and Cargo dependency discovery, workspace handling, lockfile diagnostics, fixtures, and CLI integration implemented
  - Phase 4 npm, PyPI, and Cargo metadata adapters, repository normalization, source evidence, timestamps, allowlists, fixtures, and tests implemented
  - Phase 5 package funding metadata, GitHub FUNDING.yml, public provider-response parsing, provenance, diagnostics, fixtures, and tests implemented
  - Phase 6 package/repository/funding relationship resolution, confidence, ambiguity, contradiction, unresolved states, fixtures, and tests implemented
  - Phase 7 deterministic report document, text/JSON renderers, stable ordering, summaries, evidence drill-down, limitations, action links, fixtures, and CLI integration implemented
  - Phase 8 typed network errors, bounded retries, rate-limit backoff, opt-in TTL cache, cache invalidation, offline replay, cancellation, and partial-result batch semantics implemented and tested
  - Phase 9 trust-boundary audit, secure URL and redirect policy, response/cache resource limits, authenticated-cache protection, adversarial fixtures, dependency audit, and residual-risk documentation completed
  - Phase 10 executable fixture matrix, npm/PyPI/Cargo end-to-end pipeline tests, failure-category coverage, deterministic repeat-run checks, and shared-fixture CLI smoke tests completed
  - Phase 11 cross-platform CI workflows, Node 20/22 matrices, lint/typecheck/test/build/package checks, sibling-core CLI installation verification, and npm artifact jobs completed
  - Phase 12 v0.1 documentation/demo verification, release notes, final audit, local artifact installation checks, and release limitations completed
  - Phase 13 external contributor issue/PR templates, adapter and fixture guide, compatibility policy, good-first issues, and maintainer runbook completed
  - Phase 14 baseline Go module discovery, malformed-input coverage, CLI integration, compatibility documentation, and explicit future-scope boundaries completed
  - Phase 15 explicit core orchestration and CLI --network opt-in for npm/PyPI/Cargo metadata, funding evidence, relationship resolution, and deterministic reports completed
  - Public FundGraph organization and three repositories verified on GitHub
  - Remote CLI CI verified across Ubuntu, Windows, and macOS on Node 20 and Node 22, including package artifact creation
  - Independent engineering and security audit completed; findings recorded in AUDIT_REPORT.md
  - Audit corrections merged through GitHub pull requests into all three main branches
  - Audit branches deleted remotely and locally after merge verification
  - Published @fundgraph/core@0.1.0 to npm
  - Published fundgraph@0.1.1 to npm with the Windows executable fix
  - Merged the CLI Windows entrypoint fix through PR #9 as commit ff189c1
  - Verified clean global installation, fundgraph --version, and fundgraph --help on Windows
in_progress: []
blocked: []
next_phase: 16+
next_recommended_action: Prepare the factual Drips/GrantFox submission, collect real usage feedback, and define Phase 16 before adding features
release_target: npm @fundgraph/core@0.1.0 and fundgraph@0.1.1 published; no GitHub release/tag claimed
known_risks:
  - Deadline leaves little time for broad ecosystem support
  - Registry metadata and repository links can be stale or contradictory
  - Lockfile formats and workspace semantics vary by ecosystem
  - Network services can rate-limit or fail
  - CLI has no committed package-lock.json until the @fundgraph/core publication dependency is resolved
  - GitHub release/tag creation and funding-program submission remain owner-controlled actions
  - GitHub repository topics and organization profile metadata remain unset
  - Go metadata/funding and non-GitHub funding-file orchestration remain out of scope
  - Funding URLs require human review and do not establish maintainer identity or legitimacy
  - Latest local audit pass could not inspect the live GitHub API; PR, ruleset, and organization status require re-verification
```

State is updated after every phase. This file is both human-readable and intentionally simple to parse.
