# FundGraph v0.1.0 Final Audit

Date: 2026-10-09
Status: public repository release candidate; npm publication and merge/release governance remain pending

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

- `fundgraph-core`: lint, typecheck, build, and 40 tests passed locally.
- `fundgraph-cli`: lint, typecheck, build, and 6 tests passed locally.
- Core clean installation with `npm ci` passed.
- CLI installation through the documented sibling-core development path passed.
- Core and CLI `npm pack --dry-run` checks passed.
- Both generated npm tarballs installed successfully in isolated temporary projects; the packaged CLI reported version `0.1.0` and exposed its executable bin entries.
- README/demo commands and CLI help/error/report behavior were checked against the current implementation.
- CLI Go fixture smoke test passed with three discovered Go dependencies and no diagnostics.
- Phase 9 production dependency audits reported zero vulnerabilities. A fresh audit was attempted during this handoff but
  npm's Windows cache/registry endpoint failed before returning a result; that infrastructure failure is not treated as a
  new vulnerability finding.
- CI workflows define Ubuntu, Windows, and macOS jobs on Node 20 and Node 22, but remote CI has not run because no GitHub remotes exist.

## Incomplete or deliberately pending work

- The packages have not been published to npm.
- The GitHub organization and three public repositories exist, and the local repositories track their `main` branches.
- Remote CI has run successfully for `fundgraph-cli`; the current audit records the accessible organization state and limitations in `AUDIT_REPORT.md`.
- The CLI's default directory analysis is local/offline; live provider orchestration is not wired into the user-facing command.
- Signing/provenance publication and final external release review remain maintainer actions.

## Known limitations

Funding declarations are evidence of published claims, not endorsements or proof of current maintainer status. FundGraph
does not infer human identity, move money, manage wallets, donate, or execute actions. Registry and repository metadata can
be stale, missing, malformed, or contradictory. Public services can fail or rate-limit requests. DNS rebinding and
deployment-specific network policy remain caller/operational responsibilities as documented in `SECURITY_AUDIT.md`.

## Security findings

No unresolved high-risk finding was identified in the Phase 9 audit. The implementation rejects unsafe/local destinations
and redirects by default, bounds response and cache resources, avoids caching authenticated requests, and preserves
explicit diagnostics for malformed or conflicting evidence. Dependency audit results for the implementation packages
reported zero production vulnerabilities during Phase 9 verification. Residual DNS and operational risks remain
documented rather than claimed solved.

## Release decision

The v0.1 acceptance criteria are satisfied for a pre-publication release candidate. The implementation, documentation,
tests, package artifacts, security controls, contributor workflow, and submission materials are ready for public release.
The release is not publicly published because the required GitHub/npm resources are external maintainer actions. No
remote, tag, or push was created by this task.

## Funding-submission readiness

The project is ready to prepare applications, but funding is never guaranteed. The application must accurately describe
FundGraph as a local-first evidence and discovery tool, not as a payment protocol. No adoption, traction, user count,
grant eligibility, or acceptance is claimed. The prepared submission brief is in `FUNDING_SUBMISSION.md`.

## Final maintainer actions

1. Review and merge the dedicated audit-fix branches; do not merge without maintainer review.
2. Publish `@fundgraph/core` before `fundgraph`, following the compatibility policy, if npm publication is desired.
3. Configure branch protection/rulesets, repository topics, organization profile metadata, Dependabot/security reporting, and any release provenance settings not yet enabled.
4. Claim the public GitHub project on Drips if applying to an eligible round.
5. Add the public repository and scoped contribution opportunities to GrantFox if the relevant campaign accepts them.

The original local publication steps have been completed. The remaining steps are maintainer decisions or settings that this audit did not change.
