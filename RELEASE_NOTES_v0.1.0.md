# FundGraph v0.1.0 release notes

Status: published package baseline. `@fundgraph/core@0.1.0` and `fundgraph@0.1.1` are available on npm.

## Included

- Local npm, PyPI, Cargo, and baseline Go module discovery.
- Workspace, alias, optional-dependency, transitive-edge, malformed-lockfile, and missing-lockfile handling.
- Recorded registry metadata normalization with source evidence.
- Package funding metadata, GitHub `FUNDING.yml`, and recorded public-provider parsing.
- Explainable package/repository/funding relationships with supported, ambiguous, contradictory, and unresolved states.
- Deterministic text and JSON reports with evidence drill-down, limitations, diagnostics, and informational actions.
- Opt-in network reliability API with bounded retries, rate-limit handling, cache TTL/invalidation, offline replay, and partial results.
- Secure URL/redirect policy, response/cache resource limits, and authenticated-cache protection.
- Cross-platform CI definitions and npm package artifacts.
- Contributor issue/PR templates, adapter guidance, compatibility policy, and maintainer runbook.

## Deliberate limitations

- The current CLI directory analyzer is local/offline by default; explicit `--network` fetches public registry metadata and GitHub `FUNDING.yml` evidence for the implemented npm, PyPI, and Cargo pipeline.
- Funding endpoints are declarations to review, not verified payment destinations or endorsements.
- FundGraph does not identify or verify individual humans, move money, manage wallets, or execute payments.
- DNS rebinding protection is a deployment responsibility; explicit host allowlists are available for network callers.
- GitHub release/tag creation and release signing remain maintainer actions.
- Non-GitHub repository funding-file retrieval is not yet orchestrated.
- Funding URLs require human review; FundGraph does not verify legitimacy or maintainer identity.
- Live GitHub organization, ruleset, and campaign requirements must be rechecked before submission.

## Verification

The release was verified locally on Windows with core lint/typecheck/build, 41 core tests, CLI lint/typecheck/build, 6 CLI tests, `npm ci` for core, sibling-core CLI installation, Go fixture CLI smoke analysis, package dry-runs, and production dependency audits. CI is configured for Ubuntu, Windows, and macOS on Node 20 and Node 22. A clean global installation of `fundgraph@0.1.1` was verified; GitHub release/tag creation and funding-program submission remain maintainer-controlled actions.
