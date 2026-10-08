# Testing strategy

Tests are fixture-first and deterministic. Unit tests cover model validation, parsers, URL normalization, confidence rules, error taxonomy, and serializers. Integration tests run complete fixture projects through the library and CLI. Golden tests lock stable report output.

Required fixture categories: funded, unfunded, multiple sources, contradictory metadata, missing repository, malformed lockfile, aliases, workspaces, optional dependencies, rate limits, and network failure. Fixtures must be synthetic or public and must not contain credentials.

The core commands are `npm run typecheck`, `npm test`, `npm run build`, and `npm pack --dry-run` in `fundgraph-core`. Phase 10 has thirty-eight core tests covering the model contract, dependency discovery, metadata normalization, funding evidence, relationship resolution, deterministic reports, network retries/cache behavior, secure URL and redirect policy, response limits, authenticated-cache bypass, partial batch results, cancellation, the complete fixture matrix, all three ecosystem pipelines, failure categories, and deterministic repeat runs. The CLI has six tests covering its command contract, report integration, directory discovery, and shared-fixture smoke behavior. Dependency review uses `npm audit --omit=dev --package-lock=false` in both implementation repositories.

