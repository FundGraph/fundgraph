# Release checklist

Before v0.1.0, verify all of the following:

- [ ] Phase 0–12 acceptance and exit criteria are met or explicitly re-scoped.
- [ ] `npm run lint`, `npm run typecheck`, `npm test`, and `npm run build` pass on a clean checkout.
- [ ] CLI help, examples, error paths, and report output work on Windows, macOS, and Linux or have documented limits.
- [ ] Fixtures cover funded, unfunded, multiple, contradictory, missing, malformed, alias, workspace, optional, rate-limit, and network-failure cases.
- [ ] No credentials, private source, generated secrets, or unreviewed placeholders are committed.
- [ ] README installation and commands are verified against the released artifact.
- [ ] `FINAL_AUDIT.md`, release notes, changelog, license, security policy, and contribution guide are current.
- [ ] A GitHub organization/repository is created by the maintainer separately; only then may a remote be added and push authorized.

