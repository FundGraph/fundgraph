# FundGraph funding submission brief

This document is a factual preparation brief for Drips, GrantFox, and similar open-source funding programs. It is not a
claim of eligibility, acceptance, traction, or endorsement.

## One-sentence pitch

FundGraph is an open-source local-first CLI and TypeScript library that maps project dependencies to declared funding
pathways and shows the evidence and uncertainty behind each relationship.

## Problem

Developers and funders can often find isolated funding links in package metadata or repository pages, but it is difficult
to connect a real dependency graph to package identity, repository identity, funding declarations, provenance, and
conflicting evidence in one reviewable result. This makes OSS sustainability analysis manual and easy to overstate.

## Solution

FundGraph reads local dependency inputs, normalizes package and repository identities, preserves funding declarations as
evidence, resolves relationships without inferring human identity, and emits deterministic text/JSON reports. It is
useful without credentials and does not move money, manage wallets, execute payments, or automatically donate.

## Current implementation

- npm, PyPI, Cargo, and baseline Go module dependency discovery.
- Recorded npm/PyPI/Cargo metadata and funding evidence providers.
- Explicit supported, ambiguous, contradictory, and unresolved relationship states.
- Deterministic reports with evidence drill-down and limitations.
- Secure, opt-in network primitives with bounded retries, cache controls, and offline replay.
- TypeScript core library plus `fundgraph` CLI in three independent repositories.
- 40 core tests and 6 CLI tests passing locally, with lint/typecheck/build/package checks.

## Why public-good funding would help

Funding would support maintenance of a neutral evidence layer for open-source sustainability analysis. The work benefits
maintainers, engineering teams, OSS funders, and researchers who need a more careful answer than a list of unverified
funding URLs. The project also aims to improve visibility for dependencies that are frequently used but difficult to
fund through existing workflows.

## Proposed milestones

These are proposed work packages, not completed work:

1. **Public release and validation:** publish the three repositories, run remote CI, publish compatible npm artifacts,
   and collect feedback from maintainers.
2. **Evidence coverage:** add more recorded ecosystem/provider fixtures and improve contradiction and missing-data reports.
3. **Contributor growth:** maintain contributor documentation, add bounded issues, and review external adapter/fixture PRs.
4. **Reproducible sustainability reports:** improve offline snapshots or export integrations only after real user demand.

## Measurable deliverables

- Public repositories with reproducible CI and release artifacts.
- New recorded fixtures and tests merged under the evidence/security rules.
- Issue and pull-request history showing external review and contributor participation.
- Published release notes and compatibility records for each supported package version.
- Demonstrations using public fixtures, with no fabricated adoption or funding numbers.

## Drips positioning

Drips describes RetroPGF applications as being submitted on behalf of a claimed GitHub Project, with round-specific fields
and public/private visibility rules. FundGraph should therefore be submitted only after its public GitHub repository is
created and claimed, and only to a round whose category and questions fit the project. FundGraph is complementary to
Drips: it analyzes and explains funding pathways; it does not implement Drips payment flows.

## GrantFox positioning

GrantFox presents itself as an open-source collaboration ecosystem where projects publish opportunities and contributors
discover issues, contribute, build reputation, and earn rewards. FundGraph should be presented with concrete public
contribution opportunities—fixtures, parser improvements, documentation, and tests—rather than as a request based only
on an idea or private roadmap. Campaign-specific rules must be checked at submission time.

## Honest limitations

The project has no claimed external adoption, usage metrics, revenue, prior funding, or acceptance. The local release
candidate is not the same as a public release. Funding declarations are not endorsements or proof of current maintainer
status. The CLI directory workflow is offline/local by default, and Go metadata/funding support is not yet implemented.
