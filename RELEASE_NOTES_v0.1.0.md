# FundGraph v0.1.0 release notes

Status: pre-publication release candidate; technically ready for publication after maintainer GitHub setup.

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

- The current CLI directory analyzer is local/offline and does not silently fetch live registry or provider data.
- Funding endpoints are declarations to review, not verified payment destinations or endorsements.
- FundGraph does not identify or verify individual humans, move money, manage wallets, or execute payments.
- DNS rebinding protection is a deployment responsibility; explicit host allowlists are available for network callers.
- GitHub organization/repositories, npm publication, and release signing remain maintainer actions.

## Verification

The release candidate was verified locally on Windows with core lint/typecheck/build, 40 core tests, CLI lint/typecheck/build, 6 CLI tests, `npm ci` for core, sibling-core CLI installation, Go fixture CLI smoke analysis, package dry-runs, and production dependency audits. CI is configured for Ubuntu, Windows, and macOS on Node 20 and Node 22 but has not run remotely because no GitHub remotes exist yet.
