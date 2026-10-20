# Phase 19 validation record

Date: 2026-10-20
Status: partially complete

## Purpose

Phase 19 validates FundGraph with a real public-package workflow before any new ecosystem or provider expansion. It is
specifically intended to test multi-provider evidence, incomplete and conflicting observations, staleness handling, and
whether a real user can rely on the output for a funding-related decision.

## Reproducible workflow

The permanent input is [`examples/phase-19-public-funding`](examples/phase-19-public-funding), which contains a small
owner-controlled npm project with pinned `eslint@9.37.0` and `prettier@3.6.2` dependencies and a committed lockfile.

The network-enabled command was run from the CLI build with the local Phase 19 core fix installed:

```text
node dist/main.js analyze C:\Users\user\Projects\FundGraph\fundgraph\examples\phase-19-public-funding --network --format json
```

Observed result:

- exit code: `1` because the report contained network diagnostics (partial result semantics)
- dependency count: `88`
- package records: `85`
- funding sources: `10`
- evidence records: `170`
- npm version-specific metadata requests completed without the earlier oversized packument failures

Observed declared funding URLs included eslint.org, Open Collective, GitHub Sponsors, and repository links for the
resolved packages. These are published declarations, not endorsements or proof of maintainer identity.

## Diagnostics and interpretation

- Several GitHub `FUNDING.yml` requests returned HTTP `403`. This is an external unauthenticated API access/rate-limit
  limitation in the run. The result is retained as a network diagnostic; it is not treated as proof that a repository
  has no funding file.
- One `npm:lodash-merge` metadata request returned HTTP `404`. This is retained as a missing/changed registry record,
  not converted into a guessed package identity or funding relationship.
- The workflow therefore demonstrates useful partial results and explicit uncertainty, but not complete provider
  coverage for every dependency.

## Correctness evidence

Recorded provider tests in `fundgraph-core` cover npm, PyPI, and Cargo provenance, parser identity, raw payload retention,
observation timestamps, HTTPS funding declarations, and point-in-time snapshot semantics. Existing funding and
relationship fixtures cover multiple sources and contradictory evidence. Cache tests cover fresh and stale observations.

The npm orchestration fix was merged through `fundgraph-core` PR #12 as `93dc71ca25c4ab29594f5c43c01aed89063ac440`.
It changes resolved npm metadata requests to bounded version-specific endpoints. Local core lint, typecheck, all 45
tests, and package dry-run passed; GitHub Actions `fundgraph-core CI` completed successfully for the PR head. The fix is
not yet claimed as published under a new npm version.

An authenticated `npm publish --access public` attempt for `@fundgraph/core@0.1.2` reached npm but was stopped by the
account's required one-time password (`EOTP`). No publication is claimed until the owner completes that browser/2FA
step and verifies `npm view @fundgraph/core@0.1.2 version`.

## External-user validation

No independent external user, maintainer, funder, or researcher has yet supplied a reproducible workflow or confirmed
that a FundGraph report changed a funding decision. No adoption, provider reliability, or decision-impact claim is made.
This is the remaining substantive Phase 19 acceptance gap and requires real owner-supplied feedback before Phase 19 can
be marked complete.

## Next evidence required

The owner should provide one real reviewer and one public or non-sensitive project workflow. Record the input class,
command, observed report, whether conflicts/staleness affected interpretation, and whether the report changed a concrete
funding or maintenance action. Do not upload private source or credentials. Do not create issues or claim adoption from
one review.
