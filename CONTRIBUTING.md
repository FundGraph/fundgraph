# Contributing to FundGraph

FundGraph welcomes focused contributions that improve dependency analysis, evidence quality, portability, documentation, or tests.

Before coding, read `PROJECT_CONTEXT.md`, `PROJECT_STATE.md`, `ROADMAP.md`, and the relevant documents under `docs/`. Use `docs/GOOD_FIRST_ISSUES.md` for bounded starter work, `docs/ADAPTER_GUIDE.md` for core adapters, and `docs/COMPATIBILITY_POLICY.md` for public-contract changes. Keep changes small and explain any scope or model change in `DECISION_LOG.md`.

Pull requests should include tests for behavior changes, preserve deterministic ordering, avoid private data, and update user-facing documentation. Do not add payment execution, wallet handling, identity inference, or opaque AI decisions.

Use the commands documented in `docs/TESTING.md` and report the exact environment and results. For governance questions,
security escalation, and release handoff, use `docs/MAINTAINER_RUNBOOK.md`.

