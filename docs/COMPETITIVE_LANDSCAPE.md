# Competitive landscape

Research snapshot: 2026-10-08.

| Tool/mechanism | What it does | FundGraph distinction |
|---|---|---|
| `npm fund` | Displays funding URLs from npm dependency metadata, including a tree and workspace filtering. | Cross-ecosystem graph, repository/evidence chain, conflicts, confidence, and deterministic reports. |
| `libnpmfund` | Node library that reads npm Arborist trees and returns funding-bearing package nodes. | FundGraph is not npm-only and preserves evidence/relationship semantics beyond a funding tree. |
| GitHub Sponsors / `FUNDING.yml` | Provides sponsor links for repositories, including GitHub Sponsors and external platforms. | FundGraph consumes declarations as evidence; it does not create sponsor buttons or process sponsorships. |
| Open Collective | Platform for communities to collect, manage, and disburse money, with public documentation/API. | FundGraph may identify links but does not manage money or act as a collective. |
| Drips | Funding protocol/app with dependency splitting and recurring or one-time support. | FundGraph is a discovery and evidence layer, not an on-chain funding protocol. |
| Registry metadata | npm/PyPI/Cargo package metadata can contain repository and funding fields. | FundGraph normalizes and cross-checks these fields, retaining provenance and disagreement. |
| Dependency graph tools | Resolve packages and versions for build/audit purposes. | FundGraph uses the graph to answer funding-pathway questions, not merely dependency inventory. |

Sources: [npm fund](https://docs.npmjs.com/cli/v12/commands/npm-fund/), [libnpmfund](https://www.npmjs.com/package/libnpmfund), [GitHub funding files](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/displaying-a-sponsor-button-in-your-repository), [Open Collective docs](https://documentation.opencollective.com/), and [Drips dependency funding](https://www.drips.network/solutions/dependency-funding).

The idea is adjacent to existing tools, not empty. The defensible niche is a local-first, evidence-preserving, cross-ecosystem analysis/reporting layer that deliberately stops before payment execution.

