# Phase 17 Validation — Release Metadata and Compatibility Hardening

Date: 2026-10-19
Status: complete

## Scope

Phase 17 addressed the concrete release-polish findings from Phase 16 without
adding ecosystems, providers, contributor issues, or payment functionality.

## Completed

- `@fundgraph/core` was published as `0.1.1` and is publicly readable from npm.
- `fundgraph` was published as `0.1.2` and is publicly readable from npm.
- The CLI package now exposes canonical repository, homepage, bugs, keywords,
  Node.js engine, public-access, and executable metadata.
- The CLI now commits a registry-resolved `package-lock.json` pinned to
  `@fundgraph/core@0.1.1`.
- CLI package metadata regression coverage was added.
- The normal CLI PR path was used: PR #10 merged to `main` as
  `ed3e2e02d9b2666f4400c751c8aab7089d4d92e5`.

## Verification

Local CLI validation passed:

```text
npm ci
npm run lint
npm run typecheck
npm test
npm pack --dry-run
npm ls @fundgraph/core --depth=0
```

GitHub Actions passed for Ubuntu, Windows, and macOS on Node 20 and Node 22,
including both package-artifact jobs.

Public registry verification passed:

```text
npm view fundgraph@0.1.2 version       -> 0.1.2
npm view fundgraph@0.1.2 dist-tags ... -> latest 0.1.2
```

The clean Windows global-install smoke test passed:

```text
npm uninstall -g fundgraph
npm install -g fundgraph@0.1.2
fundgraph --version                   -> 0.1.2
fundgraph --help                      -> command contract rendered
npm ls -g fundgraph @fundgraph/core --depth=2
                                      -> fundgraph@0.1.2 / @fundgraph/core@0.1.1
```

## Remaining limitations

- Go metadata and Go funding providers are not implemented.
- Non-GitHub repository funding-file retrieval is not yet orchestrated.
- Funding URLs remain declarations requiring human review; the tool does not
  verify legitimacy or maintainer identity.
- No external adoption, maintainer feedback, or funding acceptance is claimed.
- GitHub release/tag creation and Drips/GrantFox submission remain owner-controlled.

## Decision

The Phase 16 package discoverability and reproducibility findings are resolved.
Future work should be selected from real usage evidence rather than adding an
ecosystem speculatively.
