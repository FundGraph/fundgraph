# Phase 16 validation record

Date: 2026-10-19

Status: complete for the documented acceptance criteria, with release-polish findings recorded below.

## Scope

Phase 16 validates the published npm package workflow, representative offline analysis, deterministic output, package
compatibility, security boundaries, and factual submission materials. No contributor issues were created and no new
ecosystem or provider was implemented.

## Commands and verified results

### Published package installation

```text
npm uninstall -g fundgraph
npm install -g fundgraph@0.1.1
fundgraph --version
fundgraph --help
```

Result: passed. The CLI returned `0.1.1` and rendered the documented command/help contract. The installed dependency tree
contained `@fundgraph/core@0.1.0`.

Registry verification also returned:

- `@fundgraph/core@0.1.0`
- `fundgraph@0.1.1`

### Deterministic fixture analysis

The published CLI analyzed `fundgraph-core/test/fixtures/npm-workspace` with:

```text
fundgraph analyze <fixture> --format json --offline
```

Result: passed with 4 models, 4 edges, npm ecosystem detection, and zero diagnostics. Two repeated JSON runs produced
the same SHA-256 digest:

```text
7E78CDDB7AF97E5490BC9E1998E1C9EB38D218A14178D16862D35BD11681AE1F
```

### Representative project analysis

- `fundgraph-core`: exit 0, 23 models, 3 edges, npm ecosystem, zero diagnostics.
- `fundgraph-cli`: exit 1 with 3 models, 3 edges, npm ecosystem, and one explicit `LOCKFILE_MISSING` diagnostic.

The CLI result is an expected partial analysis because `fundgraph-cli` has no committed `package-lock.json`. The behavior
is documented and no dependency version was guessed.

### Implementation verification

`fundgraph-core`:

- lint: passed
- typecheck: passed
- build: passed
- tests: 41 passed, 0 failed
- package dry-run: passed

`fundgraph-cli`:

- lint: passed
- typecheck: passed
- build: passed
- tests: 6 passed, 0 failed
- package dry-run: passed

## Security and privacy review

The validation used offline analysis for local projects. No private source was sent to a service. Network access remained
explicit rather than implicit. Existing URL allowlists, response bounds, cache controls, evidence uncertainty, and
non-payment behavior remain unchanged.

## Findings

1. **P1 release metadata:** the published package metadata does not currently expose repository URLs through npm metadata.
   The packages install and execute correctly, but future patch releases should add verified repository fields.
2. **P1 compatibility/reproducibility:** `fundgraph-cli` has no committed package lockfile. This is a documented project
   decision/risk, but it means repository analysis reports `LOCKFILE_MISSING` and clean dependency reproducibility is weaker
   than in core.
3. **No external adoption evidence:** this phase validated owner-controlled local repositories and fixtures. It did not
   claim external users, maintainer feedback, adoption, or funding-program eligibility.

## Phase decision

The Phase 16 acceptance criteria are satisfied: published packages install, documented commands work, representative
analysis is reproducible, the partial result is classified, submission materials contain verified facts, and no new scope
was selected without evidence. The findings above remain inputs to the proposed Phase 17 and are not silently treated as
resolved.

## Next action

Review the Phase 17 proposal in `ROADMAP.md`. Do not implement ecosystem expansion until the owner approves the release
metadata/lockfile direction and real usage evidence supports it.
