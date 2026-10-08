# FundGraph project context

## Mission

FundGraph is a local-first TypeScript CLI and library that analyzes a project's dependency graph and identifies legitimate funding pathways for dependencies, with evidence explaining each relationship.

## User and problem

The primary user is a developer, maintainer, security-minded engineering team, or OSS funder who needs to answer: “Who maintains the open-source software I depend on, where can they be funded, and what evidence supports that relationship?” Existing package-manager funding commands expose isolated links; FundGraph connects dependency identity, repository identity, funding endpoints, evidence, and confidence in a reviewable report.

## Solution and non-goals

FundGraph discovers dependencies, resolves package-to-repository relationships, collects declared funding evidence, records conflicts, and emits deterministic reports. It does not move money, manage wallets, execute payments, automatically donate, infer human identity, or use AI as an authority.

## Technology and principles

- TypeScript on Node.js, with a clean library/core and CLI boundary.
- Local-first: source manifests and lockfiles are analyzed locally; network access is explicit, bounded, and explainable.
- Evidence-first: every funding claim has provenance, retrieval metadata, and confidence.
- Deterministic where correctness permits: stable ordering, versioned schemas, fixtures, and reproducible reports.
- Small vertical slices over speculative infrastructure.
- Unsupported or contradictory claims remain visible rather than being silently merged.

## Current status

Phase 0 documentation and repository foundation are complete. Implementation has not started. v0.1 is planned for npm, PyPI, and Cargo, subject to Phase 1 validation.

## Relationship to other projects

FundGraph is an independent repository. It is not a monorepo with Stellar Forge, VerifyAgent, or StellarReplay. Lessons carried forward are to keep scope narrow, make evaluation easy, preserve deterministic behavior, document security boundaries, and avoid inventing reasons for past funding outcomes.

## Rules for future agents

1. Read this file, `PROJECT_STATE.md`, `ROADMAP.md`, and the relevant phase documents before major work.
2. Do not expand v0.1 ecosystems or turn the product into a payment system without a documented decision.
3. Do not silently choose between conflicting code and documentation; record the discrepancy.
4. Do not claim identity, ownership, adoption, funding, or security guarantees without evidence.
5. Update state, roadmap status, changelog, tests, and docs when a phase changes behavior.
6. Do not send private source code or credentials to external services.

