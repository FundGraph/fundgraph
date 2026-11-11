# Public verification

This page is the reproducible, public proof path for FundGraph. It links the project documentation to the independently published library and CLI without claiming that a declared funding URL is legitimate or endorsed.

## Public components

- [Project source of truth](https://github.com/FundGraph/fundgraph)
- [Reusable core library](https://github.com/FundGraph/fundgraph-core)
- [CLI repository](https://github.com/FundGraph/fundgraph-cli)
- [`@fundgraph/core` on npm](https://www.npmjs.com/package/@fundgraph/core) — verified package version `0.1.2`
- [`fundgraph` on npm](https://www.npmjs.com/package/fundgraph) — verified package version `0.1.3`

## Clean-user verification

The following uses the published CLI and a repository-local fixture. It does not need a GitHub token or any private source code.

```powershell
npm install -g fundgraph@0.1.3
fundgraph --version
Get-Content .\examples\public-verification\funding-evidence-model.json | fundgraph analyze --format json --offline
```

Expected version output:

```text
0.1.3
```

The command reads the JSON model from standard input because the published CLI accepts an omitted input path for stdin. The same fixture can be analyzed from a file path:

```powershell
fundgraph analyze .\examples\public-verification\funding-evidence-model.json --format json --offline
```

The committed [expected summary](examples/public-verification/expected-summary.json) and [resulting report](examples/public-verification/report.json) make the output inspectable without running the command.

## What the proof demonstrates

The fixture is synthetic and intentionally small. Its report demonstrates:

1. A runtime dependency discovered in an npm project model.
2. The package-to-repository relationship.
3. Funding declarations from package metadata and a repository funding file.
4. Source URLs, parser labels, and `observedAt` timestamps for provenance.
5. A contradictory provider response preserved as `status: "contradictory"` with `unknown` confidence.
6. Deterministic offline JSON output, with no network request required.
7. Report limitations and human-review actions.

The `example` identities and `.test` URLs are deliberately non-real examples. They are not endorsements, maintainer-identity claims, or evidence about an actual package.

## Determinism check

Run the same stdin command twice and compare the output files:

```powershell
Get-Content .\examples\public-verification\funding-evidence-model.json | fundgraph analyze --format json --offline > report-a.json
Get-Content .\examples\public-verification\funding-evidence-model.json | fundgraph analyze --format json --offline > report-b.json
Compare-Object (Get-Content .\report-a.json) (Get-Content .\report-b.json)
```

No comparison rows means the serialized reports are identical for the same input and published CLI version.

## Boundaries and limitations

- Funding URLs are declarations requiring human review; FundGraph does not verify legitimacy or maintainer identity.
- FundGraph does not move money, manage wallets, or execute donations.
- This fixture proves report mechanics, not provider freshness, real-world adoption, or a funding decision.
- The recorded `observedAt` timestamp is part of the evidence record; live provider data can change after retrieval.
- The report is evidence-preserving analysis, not a universal dependency resolver or recommendation engine.
