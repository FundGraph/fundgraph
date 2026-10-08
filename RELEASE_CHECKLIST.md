# Release checklist

Before v0.1.0, verify all of the following:

- [x] Phase 0–12 acceptance and exit criteria are met or explicitly re-scoped.
- [x] `npm run lint`, `npm run typecheck`, `npm test`, and `npm run build` pass locally in both implementation repositories.
- [x] CLI help, examples, error paths, and report output work on Windows, macOS, and Linux or have documented limits.
- [x] Fixtures cover funded, unfunded, multiple, contradictory, missing, malformed, alias, workspace, optional, rate-limit, and network-failure cases.
- [x] No credentials, private source, generated secrets, or unreviewed placeholders are committed.
- [x] README installation and commands are verified against the locally installed release artifact.
- [x] `FINAL_AUDIT.md`, release notes, changelog, license, security policy, and contribution guide are current.
- [ ] A GitHub organization/repository is created by the maintainer separately; this external prerequisite is intentionally pending. No remote or push is authorized yet.

