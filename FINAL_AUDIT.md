# FundGraph v0.1.0 Final Audit

Date: 2026-10-19
Status: published npm package baseline with post-publication validation; end-to-end opt-in analysis is implemented, while GitHub release/tag governance remains pending

## Scope

This audit covers the three-repository FundGraph workspace:

- `fundgraph`: project governance, release coordination, documentation, examples, and cross-repository state.
- `fundgraph-core`: reusable TypeScript library and domain/evidence/reporting implementation.
- `fundgraph-cli`: the `fundgraph` executable and CLI integration.

## Completed features

- Versioned domain models, validation, deterministic serialization, and typed errors.
- Local npm, PyPI, Cargo, and baseline Go module discovery, including documented workspace, alias, optional, and malformed-input behavior.
- Recorded registry metadata normalization with repository identity evidence.
- Funding declarations from package metadata and GitHub `FUNDING.yml`, with provenance and contradiction preservation.
- Explicit relationship resolution with confidence, ambiguity, contradiction, and unresolved states.
- Deterministic text and JSON reports with evidence references, diagnostics, limitations, and review actions.
- Opt-in network reliability primitives with retries, rate-limit handling, cache policy, cancellation, and offline replay.
- Security controls for URL destinations, redirects, payload/cache limits, and authenticated-cache handling.
- Cross-platform CI definitions, package checks, and release artifact jobs.
- External contributor onboarding, issue/PR templates, adapter guidance, compatibility policy, and maintainer runbook.

## Verification results

- `fundgraph-core`: lint, typecheck, build, and 41 tests passed locally; two cache tests are environment-blocked under the restricted Windows sandbox because atomic rename is denied.
- `fundgraph-cli`: lint, typecheck, build, and 6 tests passed locally.
- Core clean installation with `npm ci` passed.
- CLI installation through the documented sibling-core development path passed.
- Core and CLI `npm pack --dry-run` checks passed.
- Both generated npm tarballs installed successfully in isolated temporary projects; the published CLI `fundgraph@0.1.1` and core `@fundgraph/core@0.1.0` were also installed through npm.
- A clean Windows global-install smoke test passed: `fundgraph --version` returned `0.1.1` and `fundgraph --help` rendered the command contract.
- README/demo commands and CLI help/error/report behavior were checked against the current implementation.
- CLI Go fixture smoke test passed with three discovered Go dependencies and no diagnostics.
- Phase 9 production dependency audits reported zero vulnerabilities. A fresh audit was attempted during this handoff but
  npm's Windows cache/registry endpoint failed before returning a result; that infrastructure failure is not treated as a
  new vulnerability finding.
- CI workflows define Ubuntu, Windows, and macOS jobs on Node 20 and Node 22; repository remotes exist and remote CI status is maintained in `AUDIT_REPORT.md`.

## Incomplete or deliberately pending work

- npm packages are published: `@fundgraph/core@0.1.0` and `fundgraph@0.1.1`.
- The GitHub organization and three public repositories exist, and the local repositories track their `main` branches.
- Remote CI has run successfully for `fundgraph-cli`; the current audit records the accessible organization state and limitations in `AUDIT_REPORT.md`.
- The CLI's default directory analysis is local/offline; explicit `--network` now orchestrates registry metadata, package funding, and GitHub `FUNDING.yml` evidence for npm, PyPI, and Cargo.
- Signing/provenance publication and final external release review remain maintainer actions.

## Known limitations

Funding declarations are evidence of published claims, not endorsements or proof of current maintainer status. FundGraph
does not infer human identity, move money, manage wallets, donate, or execute actions. Registry and repository metadata can
be stale, missing, malformed, or contradictory. Public services can fail or rate-limit requests. DNS rebinding and
deployment-specific network policy remain caller/operational responsibilities as documented in `SECURITY_AUDIT.md`.

The current release candidate also has these explicit limitations:

- Go metadata and Go funding providers are not implemented.
- Non-GitHub repository funding-file retrieval is not yet orchestrated.
- Funding URLs require human review; FundGraph does not verify legitimacy or maintainer identity.
- Live GitHub API inspection was unavailable during the latest local audit pass; current PR, ruleset, and organization claims must be rechecked before release.

## Security findings

No unresolved high-risk finding was identified in the Phase 9 audit. The implementation rejects unsafe/local destinations
and redirects by default, bounds response and cache resources, avoids caching authenticated requests, and preserves
explicit diagnostics for malformed or conflicting evidence. Dependency audit results for the implementation packages
reported zero production vulnerabilities during Phase 9 verification. Residual DNS and operational risks remain
documented rather than claimed solved.

## Release decision

The v0.1 implementation and npm package acceptance criteria are satisfied for the published package baseline. The
implementation, documentation, tests, package artifacts, security controls, contributor workflow, and submission
materials are ready for public evaluation. No GitHub release/tag or funding-program submission is claimed.

## Funding-submission readiness

The project is ready to prepare applications, but funding is never guaranteed. The application must accurately describe
FundGraph as a local-first evidence and discovery tool, not as a payment protocol. No adoption, traction, user count,
grant eligibility, or acceptance is claimed. The prepared submission brief is in `FUNDING_SUBMISSION.md`.

## Final maintainer actions

1. Decide whether to create a GitHub release/tag for the published package baseline.
2. Configure repository topics, organization profile metadata, Dependabot/security reporting, and any release provenance settings not yet enabled.
3. Claim the public GitHub project on Drips if applying to an eligible round.
4. Add the public repository and scoped contribution opportunities to GrantFox if the relevant campaign accepts them.

The npm publication steps have been completed. The audit remediation and CLI executable fix were merged through normal
pull requests. The remaining steps are maintainer decisions, platform settings, and submission actions that this audit
did not change.
