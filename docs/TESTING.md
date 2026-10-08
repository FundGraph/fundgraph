# Testing strategy

Tests are fixture-first and deterministic. Unit tests cover model validation, parsers, URL normalization, confidence rules, error taxonomy, and serializers. Integration tests run complete fixture projects through the library and CLI. Golden tests lock stable report output.

Required fixture categories: funded, unfunded, multiple sources, contradictory metadata, missing repository, malformed lockfile, aliases, workspaces, optional dependencies, rate limits, and network failure. Fixtures must be synthetic or public and must not contain credentials.

The core commands are `npm run typecheck`, `npm test`, `npm run build`, and `npm pack --dry-run` in `fundgraph-core`. Phase 6 has twenty-two core tests covering the model contract, dependency discovery, metadata normalization, funding evidence, and relationship resolution for positive, missing-repository, conflicting-repository, conflicting-funding, ambiguous, contradictory, and deterministic cases. The CLI has five tests covering its command contract and directory discovery integration.

