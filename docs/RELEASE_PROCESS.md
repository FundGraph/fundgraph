# Release process

Releases are prepared from clean tagged commits in the relevant repository. `fundgraph-core` is released first when its API changes; `fundgraph-cli` declares and tests its compatible core range. The `fundgraph` project repository coordinates the cross-repository release notes, integration verification, and overall changelog. Maintainers verify the release checklist, run CI and local commands, inspect package contents, and publish only after an honest final audit. No remote, organization, or push is created by Codex without explicit authorization.

Versioning follows SemVer once the package API exists. Domain schema changes require migration notes and compatibility decisions.

Phase 11 CI runs independently in `fundgraph-core` and `fundgraph-cli` across Ubuntu, Windows, and macOS on Node 20 and Node 22. Core is installed with its lockfile; the CLI installs the checked-out compatible sibling core package. CI uploads tarball artifacts for inspection but does not publish them.

Phase 12 verified the README/demo commands, local checks, package dry-runs, isolated tarball installation, release notes,
and final audit. The v0.1.0 candidate is ready locally but must not be described as published until the maintainer creates
the GitHub/npm resources, runs or reviews remote CI, and explicitly authorizes release publication.

