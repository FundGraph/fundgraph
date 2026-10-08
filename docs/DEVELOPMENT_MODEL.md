# Development model

The repositories are the source of truth for their owned concerns. Project-level decisions and cross-repository contracts live in `fundgraph`; library behavior lives in `fundgraph-core`; executable behavior lives in `fundgraph-cli`. Work proceeds phase-by-phase: inspect state, read relevant docs, implement the smallest complete slice, test, update documentation/state, and verify acceptance criteria. Architecture decisions go in `DECISION_LOG.md` in `fundgraph`.

Changes should follow dependency direction: implement and release compatible `fundgraph-core` changes before consuming them in `fundgraph-cli`. Do not copy core logic into the CLI. Cross-repository changes must state the required versions and update integration fixtures where applicable.

Codex is the primary engineering agent. Other assistants may help with scoped edits, but may not silently redefine architecture, evidence authority, security boundaries, or product scope.

