# Security model

## Threats

Inputs and remote metadata may be malformed, oversized, stale, contradictory, or intentionally malicious. Network services may redirect, rate-limit, fail, or expose sensitive information if requested carelessly. Dependencies may be private.

## Controls

- Read data; never execute project scripts or lockfile content.
- Require explicit network behavior and provide offline mode.
- Allowlist public hosts and protocols; validate redirects and prevent SSRF.
- Bound file size, response size, recursion, retries, and concurrency.
- Redact credentials and sensitive paths from logs and caches.
- Escape terminal and structured output.
- Treat provider metadata as evidence, not authority.
- Do not infer people, control payment, or require credentials for basic operation.

Security review is a phase deliverable, not a one-time claim. See root `SECURITY.md` for reporting.

