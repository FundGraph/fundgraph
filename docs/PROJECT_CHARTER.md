# Project charter

FundGraph is an open-source local-first CLI/library for answering where dependency funding pathways are declared and what evidence supports them.

## Product promise

Given a project and its dependency inputs, FundGraph produces a reviewable graph and report connecting dependency package, repository, funding source, evidence, and confidence. It is an analysis and discovery tool, not a financial intermediary.

## Target users

Maintainers auditing their stack; engineering teams documenting OSS sustainability; funders identifying legitimate dependencies; researchers studying funding metadata; and contributors improving ecosystem metadata.

## Principles

Evidence before assertion; deterministic output; local-first defaults; bounded public network access; explicit uncertainty; narrow scope; useful without payment integration; and documentation as long-term memory.

## v0.1 boundary

The working boundary is npm, PyPI, and Cargo with package metadata, repository metadata, GitHub funding declarations, and selected public provider links. Phase 1 may narrow this if implementation evidence requires it.

