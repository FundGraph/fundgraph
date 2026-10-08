# Phase 9 security audit

Date: 2026-10-08

## Scope

This review covers the Phase 8 network and cache boundary, model validation, CLI input/output boundaries, URL handling, report rendering, and runtime dependencies in `fundgraph-core` and `fundgraph-cli`.

## Controls verified

- Network requests require credential-free HTTPS by default; HTTP is opt-in.
- Loopback, private, link-local, localhost, and `.local` destinations are rejected.
- Explicit host allowlists are supported for provider-specific callers.
- Redirects are rejected by the default request policy; redirect targets are never followed implicitly.
- Response bodies and cache records have bounded sizes.
- Retry counts, request timeouts, and backoff are capped.
- Cache use is opt-in; authenticated requests bypass both cache reads and writes.
- Cache writes use restrictive permissions and atomic replacement; cache invalidation is explicit.
- Offline stale data remains labeled with `CACHE_STALE` rather than being presented as fresh.
- Terminal output escapes control characters and structured reports remain data-only.
- Model and metadata validators reject unsupported schemas, unsafe URLs, oversized values, and malformed shapes.
- No project scripts, lockfiles, or remote metadata are executed.

## Dependency audit

`npm audit --omit=dev --package-lock=false` reported **0 vulnerabilities** in both implementation repositories on 2026-10-08.

## Findings and residual risks

No high-risk findings remain from this review. Hostname-based private-address checks do not perform DNS resolution, so callers requiring protection against DNS rebinding must use an explicit allowlist and a controlled network environment. Redirects are rejected rather than dynamically revalidated. The CLI’s current directory analysis remains offline and does not invoke live network requests.

## Decision

Phase 9 acceptance criteria are satisfied. Residual risks are documented and are candidates for future hardening or operational guidance, not hidden guarantees.
