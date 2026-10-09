# FundGraph independent engineering and security audit

Audit date: 2026-10-09 (Africa/Lagos)

Status: complete for the locally accessible workspace and the public `FundGraph` GitHub organization. This report is an audit record, not a release approval or funding-platform endorsement.

## Scope and method

The audit compared the local filesystem, Git roots and history, configured remotes, accessible GitHub organization metadata, source code, tests, package manifests, workflows, security documentation, release documents, and current project state. No private source, credential value, or token was recorded.

## Organization and repository inventory

The accessible GitHub organization is `FundGraph` and contains exactly three public repositories:

| Repository | Responsibility | Default branch | Remote |
|---|---|---|---|
| `fundgraph` | Project governance, cross-repository architecture, roadmap, release coordination, and submission documentation | `main` | `https://github.com/FundGraph/fundgraph.git` |
| `fundgraph-core` | TypeScript library: domain models, discovery, metadata/funding evidence, resolution, reports, and library tests | `main` | `https://github.com/FundGraph/fundgraph-core.git` |
| `fundgraph-cli` | `fundgraph` executable, CLI parsing/output/exit codes, CLI tests, and executable packaging | `main` | `https://github.com/FundGraph/fundgraph-cli.git` |

The local workspace contains exactly three `.git` directories, one in each repository, and no parent `.git`. No nested submodules or additional worktrees were found. Local branches were clean and matched their cached `origin/main` commits before this audit. A direct `git fetch` attempt was unavailable because the local shell could not connect to GitHub; GitHub API and authenticated CLI queries were available, so remote repository metadata and the latest published branch state were checked separately.

## Architecture discrepancy

The actual architecture is the three-repository TypeScript architecture above. The local and GitHub evidence did not show `fundgraph-docs`, `fundgraph-action`, or a Go-based core CLI repository. Go exists only as baseline `go.mod` discovery in `fundgraph-core`; Go metadata, funding providers, and a Go CLI are not implemented.

Older project wording in decision D-0001 described a standalone repository. D-0020 records that the current public three-repository layout supersedes that wording. No architecture migration was performed or authorized. The three boundaries are coherent: the CLI imports `@fundgraph/core`, while project-level documentation coordinates the two implementation repositories.

## Verified functionality

### Implemented and verified

- `fundgraph-core` validates versioned domain models, serializes deterministically, and exposes typed errors.
- Local discovery covers npm, PyPI, Cargo, and baseline Go `go.mod` inputs. Fixtures cover aliases, workspaces, optional dependencies, transitive edges, malformed lockfiles, and malformed Go input.
- Recorded npm, PyPI, and Cargo metadata is normalized with source evidence and repository URL normalization.
- Funding declarations from package metadata and GitHub `FUNDING.yml` are parsed as evidence. Multiple and contradictory sources remain visible.
- Relationship resolution emits supported, ambiguous, contradictory, and unresolved states with evidence links and confidence rules; it does not infer human identity.
- Deterministic text and JSON reports include summaries, evidence, diagnostics, limitations, and informational actions.
- Core network primitives are opt-in and include HTTPS/credential checks, explicit host allowlists, redirect rejection, timeouts, bounded retries, response limits, cache controls, cancellation, and offline replay.
- The CLI supports `help`, `version`, and `analyze`, bounded stdin/file input, local directory discovery, text/JSON output, offline mode, strict validation, and documented exit codes.

### Partially implemented or deliberately limited

- The CLI directory workflow is local/offline and does not orchestrate live registry/provider requests. The core library has lower-level network and recorded-evidence APIs, but this is not the same as an end-to-end live CLI funding analysis.
- Go support is baseline dependency discovery only. It does not claim Go registry metadata, funding metadata, workspace, or provider support.
- Funding URLs are declarations and evidence sources, not proof of current maintainer identity, ownership, endorsement, or payment legitimacy.
- DNS rebinding protection is not complete in the library's hostname-only private-address check; callers requiring that guarantee need explicit allowlists and network-level controls.

## Highest-priority findings

### P1 — CI dependency installation was broken on the published CLI branch — corrected

Evidence: the original GitHub run failed all six matrix jobs because CI installed `fundgraph-core` before compiling its `dist` declarations. The resulting TypeScript error was `Cannot find module '@fundgraph/core'`.

Correction: the CLI workflow now builds the checked-out core repository before installing it. The CLI test also accepts the explicit CI fixture path because Actions checks out core inside the CLI workspace.

Verification: run `37856532742` passed all six verification jobs and the package artifact job across Ubuntu, Windows, and macOS on Node 20 and Node 22.

### P1 — Project state and final audit were stale after publication — corrected on audit branch

Evidence: `PROJECT_STATE.md` and `FINAL_AUDIT.md` still said that the organization, repositories, remotes, and remote CI were pending, although the public repositories existed and remote CLI CI had passed.

Correction: state, changelog, decision records, and final-audit publication wording now describe the verified public-repository state and remaining maintainer actions.

### P1 — Repository-level security reporting and dependency automation were absent — corrected on audit branch, pending review/merge

Evidence: the three GitHub repositories had no visible `SECURITY.md` in the implementation repositories and no Dependabot configuration. This creates contributor ambiguity and delays dependency/action update visibility.

Correction: concise security policies and monthly npm/GitHub Actions Dependabot configuration were added to `fundgraph-core` and `fundgraph-cli`, then merged through pull request #1 in each implementation repository.

### P1 — CLI dependency lockfile is absent — outstanding

Evidence: `fundgraph-core` has `package-lock.json` and uses `npm ci`; `fundgraph-cli` has no committed lockfile and uses `npm install` for its unpublished sibling dependency in CI. This weakens reproducibility until the core package publication contract is established.

Recommended correction: after deciding whether and where `@fundgraph/core@0.1.x` is published, generate and commit a CLI lockfile against the supported release path, then use a reproducible installation command in release CI. Do not create a misleading lockfile against a temporary local path.

### P1 — Default branches have no verified branch protection or ruleset — outstanding

Evidence: GitHub returned `Branch not protected` for `main` in all three repositories. The audit did not change branch protections.

Recommended manual action: require pull requests, required CI checks, and at least one review on each default branch before accepting public contributions. Configure this in GitHub after reviewing the repository ownership model.

### P2 — GitHub organization/repository presentation metadata is incomplete — outstanding

Evidence: organization description/profile metadata and repository topics were empty in the accessible GitHub metadata; repository descriptions and MIT licenses were present.

Recommended manual action: add the organization profile README/avatar/description and consistent topics such as `open-source`, `dependency-analysis`, `developer-tools`, `oss-sustainability`, and `typescript` where appropriate. This is presentation work, not evidence of product capability.

### P2 — Workflow actions use mutable major tags — outstanding

Evidence: workflows use `actions/checkout@v4`, `actions/setup-node@v4`, and `actions/upload-artifact@v4` rather than immutable commit SHAs.

Recommended correction: pin third-party actions to reviewed commit SHAs and let Dependabot propose updates. This should be performed with the exact SHAs reviewed by the maintainer; no unverified SHA was introduced during this audit.

## Security review

Static review and the core security tests found no confirmed P0 vulnerability. Parsers do not execute project scripts or invoke package managers/toolchains; file reads are bounded; URLs reject credentials, unsafe protocols, and common private destinations; redirects are rejected; response/cache sizes are bounded; authenticated responses are not cached; and CLI output is data-oriented.

Residual risks remain: hostname checks do not resolve DNS and therefore do not independently prevent DNS rebinding; callers must apply allowlists and network controls. Public metadata can be stale, malicious, contradictory, or unavailable. The product performs no financial transaction.

## Commands and results

- Workspace enumeration and recursive `.git` inspection: passed; exactly three repositories, no parent `.git`.
- Git status, branch, remotes, worktrees, tags, and submodules: passed; clean `main` baseline, no tags/releases, no submodules/worktrees.
- Authenticated GitHub organization/repository inventory: passed; exactly three accessible public repositories.
- `fundgraph-core`: `npm ci`, `npm run lint`, `npm run typecheck`, `npm test`, `npm run build`, and `npm pack --dry-run`: passed; 40 tests passed.
- `fundgraph-cli`: `npm run lint`, `npm run typecheck`, `npm test`, `npm run build`, and `npm pack --dry-run`: passed; 6 tests passed.
- CLI remote CI run `37856532742`: passed; six matrix jobs and package artifact job passed.
- `npm audit --omit=dev --package-lock=false`: the core audit did not return a usable result in the local shell, and the CLI audit endpoint failed in the local environment. This is not reported as zero vulnerabilities. The older zero-vulnerability claim in `SECURITY_AUDIT.md` is historical and should be re-run in a functioning network environment before release.
- Direct local `git fetch --prune origin`: unavailable during this audit because the local shell could not connect to GitHub; GitHub API metadata and cached upstream commit comparisons were available.

## GitHub operations

The audit changes were reviewed and merged through normal pull request #1 flows. The verified merge commits are `017652e` (`fundgraph`), `dab328b` (`fundgraph-core`), and `5a54c15` (`fundgraph-cli`). The remote audit branches were removed by GitHub after merge, and the local audit branches were deleted only after local `main` was fast-forwarded to the merged commits. No release, tag, force-push, or security-policy weakening was performed.

## Funding-program readiness

FundGraph has a substantiated public-good problem statement and public source code, but this audit found no evidence of adoption, users, traction, endorsements, previous funding, or acceptance. Drips and GrantFox suitability depends on their current program criteria and the project's honest description as an evidence/discovery layer. GrantFox or Stellar-specific claims require a verified program relationship; none is asserted here. The project must not present the CLI as a complete live funding orchestrator or present funding URLs as verified payment destinations.

## Final readiness assessment

- Local development: **Ready**, with documented commands and passing local checks.
- External contribution: **Conditionally ready**; the audit branch adds security reporting and Dependabot metadata, but branch protection and maintainer review rules remain to be configured.
- Public v0.1 release: **Not yet release-complete**; code and CI are healthy, but npm publication, a reproducible CLI release dependency path, branch protections, and release-owner decisions remain.
- Funding-program submission: **Conditionally ready to submit an accurate application**; the project can describe completed work and concrete contribution opportunities, but must not claim adoption, published npm packages, funding eligibility, or acceptance without evidence.

## Owner actions

1. Configure remaining branch protection/ruleset requirements and review repository security reporting in GitHub.
2. Decide the npm publication/release path, then add the CLI lockfile and provenance/release checks.
3. Re-run production dependency audits from a functioning network environment.
4. Add organization profile metadata and repository topics if desired.
5. Prepare funding submissions using the factual limitations above.
