# Project charter

FundGraph is an open-source local-first CLI/library for answering where dependency funding pathways are declared and what evidence supports them.

FundGraph is a multi-repository project consisting of three independent repositories contained within the `FundGraph` workspace. The project repository coordinates the independently publishable core library and CLI package.

## Product promise

Given a project and its dependency inputs, FundGraph produces a reviewable graph and report connecting dependency package, repository, funding source, evidence, and confidence. It is an analysis and discovery tool, not a financial intermediary.

## Target users

Maintainers auditing their stack; engineering teams documenting OSS sustainability; funders identifying legitimate dependencies; researchers studying funding metadata; and contributors improving ecosystem metadata.

## Principles

Evidence before assertion; deterministic output; local-first defaults; bounded public network access; explicit uncertainty; narrow scope; useful without payment integration; and documentation as long-term memory.

## v0.1 boundary

The v0.1 boundary is npm, PyPI, and Cargo with package metadata, repository metadata, GitHub funding declarations, and
selected public provider links. Baseline Go `go.mod` discovery is the first v1 expansion; Go metadata and funding
providers remain future scope. See `FUNDING_SUBMISSION.md` for the factual submission position.
