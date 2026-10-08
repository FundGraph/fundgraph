# FundGraph project context

## Mission

FundGraph is a local-first TypeScript CLI and library that analyzes a project's dependency graph and identifies legitimate funding pathways for dependencies, with evidence explaining each relationship.

FundGraph is a multi-repository project consisting of three independent repositories contained within the `FundGraph` workspace: `fundgraph`, `fundgraph-core`, and `fundgraph-cli`.

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

## Repository architecture

- `fundgraph`: project-level source of truth, governance, roadmap, cross-repository architecture, release coordination, examples, and integration fixtures. It is not the implementation package.
- `fundgraph-core`: independently versioned and publishable reusable TypeScript library. It owns domain models, dependency discovery, ecosystem adapters, evidence, resolution, reports, and library tests.
- `fundgraph-cli`: independently versioned and publishable executable package. It owns command parsing, terminal UX, exit codes, CLI configuration, CLI tests, and depends on a released `fundgraph-core` version.

The repositories work together as `fundgraph-cli` → `fundgraph-core`; `fundgraph` coordinates the project and validates cross-repository examples. There are no submodules, worktrees, or parent repository.

## Current status

Phases 0–13 are complete for a local v0.1.0 release candidate. The implementation supports npm, PyPI, and Cargo
discovery and evidence/reporting workflows across `fundgraph-core` and `fundgraph-cli`. The candidate is not published:
GitHub/npm resources, remote CI execution, and publication remain maintainer-owned external actions. Contributor onboarding,
adapter guidance, compatibility policy, and maintainer escalation are documented for the next phase.

## Relationship to other projects

FundGraph is independent from Stellar Forge, VerifyAgent, and StellarReplay. It is not a monorepo with those projects or with its own three repositories. Lessons carried forward are to keep scope narrow, make evaluation easy, preserve deterministic behavior, document security boundaries, and avoid inventing reasons for past funding outcomes.

## Rules for future agents

1. Read this file, `PROJECT_STATE.md`, `ROADMAP.md`, and the relevant phase documents before major work.
2. Do not expand v0.1 ecosystems or turn the product into a payment system without a documented decision.
3. Do not silently choose between conflicting code and documentation; record the discrepancy.
4. Do not claim identity, ownership, adoption, funding, or security guarantees without evidence.
5. Update state, roadmap status, changelog, tests, and docs when a phase changes behavior.
6. Do not send private source code or credentials to external services.
7. Treat `C:\Users\user\Projects\FundGraph` as a container only; never initialize Git there.
8. Changes crossing repository boundaries require updates to the owning repository documentation and compatibility notes.

