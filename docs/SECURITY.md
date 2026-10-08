# Security model

## Threats

Inputs and remote metadata may be malformed, oversized, stale, contradictory, or intentionally malicious. Network services may redirect, rate-limit, fail, or expose sensitive information if requested carelessly. Dependencies may be private.

## Controls

- Read data; never execute project scripts or lockfile content.
- Require explicit network behavior and provide offline mode.
- Allowlist public hosts and protocols; validate redirects and prevent SSRF.
- The network client defaults to credential-free HTTPS, rejects private/loopback/local destinations and redirects, supports explicit host allowlists, and bounds response bodies before JSON parsing.
- Bound file size, response size, recursion, retries, and concurrency.
- Redact credentials and sensitive paths from logs and caches.
- Caching is opt-in, rejects authorization/cookie-bearing requests, uses URL hashes rather than raw filenames, writes files with restrictive permissions, and supports explicit invalidation. Stale offline replay is labeled rather than silently treated as fresh.
- Retry counts, timeouts, backoff, payload handling, and cache TTLs are bounded; cancellation is propagated.
- Escape terminal and structured output.
- Treat provider metadata as evidence, not authority.
- Do not infer people, control payment, or require credentials for basic operation.

Security review is a phase deliverable, not a one-time claim. See root `SECURITY.md` for reporting.

Phase 9 findings, dependency audit results, and residual risks are recorded in [`SECURITY_AUDIT.md`](../SECURITY_AUDIT.md). The audit does not claim complete SSRF protection for DNS rebinding; controlled callers must provide an allowlist and network-level controls.

