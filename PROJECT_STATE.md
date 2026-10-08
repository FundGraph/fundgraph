# Project state

```yaml
current_phase: 6
current_status: complete
last_completed_phase: 6
current_objective: Preserve explainable funding relationships and prepare deterministic reports.
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
in_progress: []
blocked: []
next_phase: 7
next_recommended_action: Execute Phase 7: Deterministic Reports
release_target: v0.1.0 by 2026-10-09T12:00:00+01:00
known_risks:
  - Deadline leaves little time for broad ecosystem support
  - Registry metadata and repository links can be stale or contradictory
  - Lockfile formats and workspace semantics vary by ecosystem
  - Network services can rate-limit or fail
```

State is updated after every phase. This file is both human-readable and intentionally simple to parse.

