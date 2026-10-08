# Contributor guide

Choose a roadmap phase or a focused backlog item, then identify the owning repository. Read the project docs in `fundgraph` and the relevant repository README/development guide. New adapters belong in `fundgraph-core`; command parsing and terminal behavior belong in `fundgraph-cli`; cross-repository examples and policy belong in `fundgraph`.

New adapters should follow `docs/ADAPTER_GUIDE.md`: return normalized entities plus evidence, include fixtures for success and failure, preserve raw source references safely, and avoid hidden network calls. A CLI pull request must not duplicate domain logic from core.

When behavior changes, update CLI docs, tests, changelog, and project state as appropriate. Use `docs/COMPATIBILITY_POLICY.md` for contract changes and `docs/MAINTAINER_RUNBOOK.md` for escalation. Keep pull requests reviewable and do not broaden product scope through implementation convenience.

