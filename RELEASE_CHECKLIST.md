# Release checklist

Before and after the v0.1 package baseline, verify all of the following:

- [x] Phase 0–14 acceptance and exit criteria are met or explicitly re-scoped.
- [x] `npm run lint`, `npm run typecheck`, `npm test`, and `npm run build` pass locally in both implementation repositories.
- [x] CLI help, examples, error paths, and report output work on Windows, macOS, and Linux or have documented limits.
- [x] Fixtures cover funded, unfunded, multiple, contradictory, missing, malformed, alias, workspace, optional, rate-limit, and network-failure cases.
- [x] No credentials, private source, generated secrets, or unreviewed placeholders are committed.
- [x] README installation and commands are verified against the locally installed release artifact.
- [x] `FINAL_AUDIT.md`, release notes, changelog, license, security policy, and contribution guide are current.
- [x] Funding-submission brief accurately states project value, milestones, limitations, and unverified claims.
- [x] `PUBLISHING_HANDOFF.md` documents the final maintainer-only GitHub/release actions without performing them.
- [x] The FundGraph organization and three public repositories exist, and the published package baseline is recorded.
- [ ] A GitHub release/tag and provenance settings are configured if the maintainer chooses to create them.
