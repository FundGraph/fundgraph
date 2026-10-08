# Testing strategy

Tests are fixture-first and deterministic. Unit tests cover model validation, parsers, URL normalization, confidence rules, error taxonomy, and serializers. Integration tests run complete fixture projects through the library and CLI. Golden tests lock stable report output.

Required fixture categories: funded, unfunded, multiple sources, contradictory metadata, missing repository, malformed lockfile, aliases, workspaces, optional dependencies, rate limits, and network failure. Fixtures must be synthetic or public and must not contain credentials.

The core commands are `npm run typecheck`, `npm test`, `npm run build`, and `npm pack --dry-run` in `fundgraph-core`. Phase 3 has eight core tests covering the model contract plus npm, PyPI, and Cargo fixtures, workspaces, aliases, optional dependencies, transitive edges, missing lockfiles, and malformed lockfiles. The CLI has five tests covering its command contract and directory discovery integration.

