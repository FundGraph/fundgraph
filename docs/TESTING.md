# Testing strategy

Tests are fixture-first and deterministic. Unit tests cover model validation, parsers, URL normalization, confidence rules, error taxonomy, and serializers. Integration tests run complete fixture projects through the library and CLI. Golden tests lock stable report output.

Required fixture categories: funded, unfunded, multiple sources, contradictory metadata, missing repository, malformed lockfile, aliases, workspaces, optional dependencies, rate limits, and network failure. Fixtures must be synthetic or public and must not contain credentials.

The core commands are `npm run lint`, `npm run typecheck`, `npm test`, `npm run build`, and `npm pack --dry-run` in `fundgraph-core`. Phase 11 retains thirty-eight core tests and six CLI tests, adds repository lint checks, and verifies both package workflows across Ubuntu, Windows, and macOS on Node 20 and Node 22. Dependency review uses `npm audit --omit=dev --package-lock=false` in both implementation repositories. The complete CI and artifact policy is documented in [`CI.md`](CI.md).

