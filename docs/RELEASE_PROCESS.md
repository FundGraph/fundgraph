# Release process

Releases are prepared from clean tagged commits in the relevant repository. `fundgraph-core` is released first when its API changes; `fundgraph-cli` declares and tests its compatible core range. The `fundgraph` project repository coordinates the cross-repository release notes, integration verification, and overall changelog. Maintainers verify the release checklist, run CI and local commands, inspect package contents, and publish only after an honest final audit. No remote, organization, or push is created by Codex without explicit authorization.

Versioning follows SemVer once the package API exists. Domain schema changes require migration notes and compatibility decisions.

