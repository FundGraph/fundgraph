# Adapter and fixture guide

This guide is for contributors adding a registry, metadata, or funding adapter to `fundgraph-core`.

## Before opening a change

1. Read `PROJECT_CONTEXT.md`, `ROADMAP.md`, `docs/ARCHITECTURE.md`, `docs/DATA_MODEL.md`, `docs/EVIDENCE_MODEL.md`, and `docs/SECURITY.md` in the sibling `fundgraph` repository.
2. Open an issue describing the ecosystem/provider, public source, expected evidence, failure behavior, and compatibility impact.
3. Confirm that the work fits the current roadmap and does not infer human identity, endorse a destination, or execute payment.

## Repository locations

- Discovery: `fundgraph-core/src/inputs/`
- Registry metadata: `fundgraph-core/src/metadata/`
- Funding declarations: `fundgraph-core/src/funding/`
- Shared models and validation: `fundgraph-core/src/domain/`
- Deterministic fixtures: `fundgraph-core/test/fixtures/`
- Tests: the matching file under `fundgraph-core/test/`

Keep parsers pure. They consume an injected payload/context and must not perform hidden network requests. Preserve the
source URL, parser identifier, observation timestamp, and bounded raw payload as evidence. Reject unsafe URLs and
oversized input through the existing validation/error patterns. Never silently merge conflicting declarations.

## Fixture-first workflow

From `fundgraph-core`:

```text
npm install
npm run lint
npm run typecheck
npm test
```

Add a small recorded fixture for each meaningful result, including at least one malformed, missing, or contradictory
case. Use stable JSON and fixed timestamps. Do not use live services in tests and do not commit credentials or private
source. Add the fixture to `test/fixtures/integration/fixture-matrix.json` when it represents a required category.

Implement the parser, add assertions for normalized entities and evidence IDs, then add a deterministic repeat-run test.
Run `npm test` twice if ordering or serialization changes. Update the relevant core README and project documentation
when the public behavior changes.

## Pull request checklist

- [ ] Issue and scope are linked.
- [ ] Recorded success and failure fixtures are included.
- [ ] Evidence retains source, parser, timestamp, and bounded raw observation.
- [ ] Contradictions remain visible; no identity is inferred.
- [ ] `npm run lint`, `npm run typecheck`, `npm test`, and `npm run build` pass.
- [ ] Security and compatibility implications are documented.
