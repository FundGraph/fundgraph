# Publishing handoff

This is the final maintainer-owned step. Codex has not created GitHub resources, added remotes, tagged releases, or pushed
commits.

## Create the public repositories

Create these three empty GitHub repositories under the maintainer's organization:

```text
GITHUB_ORG=<your-org>
GITHUB_ORG/fundgraph
GITHUB_ORG/fundgraph-core
GITHUB_ORG/fundgraph-cli
```

Do not create a fourth parent repository. The local parent `C:\Users\user\Projects\FundGraph` remains only a workspace
container.

Use [`GITHUB_REPOSITORY_METADATA.md`](GITHUB_REPOSITORY_METADATA.md) to set the GitHub About descriptions and topics for
each repository after creation.

## Add remotes and push

Run these commands from each repository after replacing `<your-org>`:

```powershell
cd C:\Users\user\Projects\FundGraph\fundgraph
git remote add origin https://github.com/<your-org>/fundgraph.git
git push -u origin main

cd ..\fundgraph-core
git remote add origin https://github.com/<your-org>/fundgraph-core.git
git push -u origin main

cd ..\fundgraph-cli
git remote add origin https://github.com/<your-org>/fundgraph-cli.git
git push -u origin main
```

## After pushing

1. Confirm the three GitHub Actions workflows complete on their supported matrix.
2. Confirm each repository has its README, license, contribution guide, and issue/PR templates.
3. Create the compatible release tags only after CI is green.
4. Publish `@fundgraph/core` before `fundgraph`, following `docs/COMPATIBILITY_POLICY.md`.
5. Claim the public GitHub repository on Drips if an eligible round is open.
6. Review the current GrantFox campaign rules and add concrete public contribution issues if the project is accepted into a campaign.

## Submission truthfulness

Before submitting, replace no claims with invented metrics. Report the actual public repository URLs, CI results, package
versions, completed milestones, and current limitations. A public release is not evidence of adoption by itself.
