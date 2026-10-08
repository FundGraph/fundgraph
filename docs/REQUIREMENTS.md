# Requirements

## Functional

1. Accept a supported project path and discover dependency inputs.
2. Normalize package and repository identities without asserting human identity.
3. Collect funding declarations and preserve their source.
4. Represent conflicts, ambiguity, missing data, and partial failures.
5. Assign explainable confidence levels.
6. Produce deterministic text and JSON reports.
7. Support offline operation from local inputs and fixtures.
8. Expose a reusable library API beneath the CLI.

## Non-functional

- TypeScript with strict typing.
- Stable versioned domain models.
- No code execution from manifests, lockfiles, or fetched metadata.
- Bounded resource use and network access.
- Cross-platform behavior documented and tested.
- Clear errors and reproducible fixtures.

## Explicit non-goals

Payments, donations, wallets, custody, automatic giving, financial advice, identity verification, package security scoring, AI-authored truth, and a web application for v0.1.

