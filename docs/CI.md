# Continuous integration and packaging

Phase 11 adds independent workflows to `fundgraph-core` and `fundgraph-cli`.

Each workflow verifies Ubuntu, Windows, and macOS against Node 20 and Node 22. The checks are:

```text
npm ci or sibling-core installation
npm run lint
npm run typecheck
npm test
npm run build
npm pack --dry-run
```

The core repository uses its committed `package-lock.json` and `npm ci`. The CLI depends on the independently released `@fundgraph/core` package contract; its workflow checks out the sibling `fundgraph-core` repository and installs that package locally so the repositories remain independently testable before publication. Local CLI development uses the same sibling installation documented in its README.

After verification, each workflow creates an npm tarball artifact. The workflows request read-only repository contents permission and do not publish packages, create releases, add remotes, or push tags.

The CI files are:

- `fundgraph-core/.github/workflows/ci.yml`
- `fundgraph-cli/.github/workflows/ci.yml`
