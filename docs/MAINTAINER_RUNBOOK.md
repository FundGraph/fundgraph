# Maintainer runbook

## Triage

1. Confirm the issue is in scope and identify the owning repository.
2. For security reports, stop public discussion and follow `SECURITY.md`.
3. Reproduce with a recorded fixture or minimal local project; never request private source when a public fixture is enough.
4. Label the issue as bug, documentation, adapter, CLI, security, or roadmap and record the affected phase.
5. If evidence is contradictory, preserve both observations and do not resolve by preference.

## Escalation and governance

Maintainers may request a design note when a change affects package identity, evidence authority, relationship confidence,
network policy, schema/API compatibility, or project scope. A maintainer may pause or re-scope work that introduces payment
execution, identity inference, opaque AI authority, credentials, or hidden network behavior. Record the decision in the
project `DECISION_LOG.md` before implementation.

If maintainers disagree, the default is to preserve the existing documented contract, open a decision issue, and defer
non-essential scope until evidence or a reproducible test supports a choice. No single contributor or assistant silently
overrides project documentation.

## Release handoff

1. Confirm the relevant repository working trees are clean and the compatibility policy is satisfied.
2. Run core checks, then CLI checks using the compatible core package.
3. Run the project integration/demo commands and inspect package contents.
4. Update changelog, release notes, project state, and `FINAL_AUDIT.md`.
5. Create tags/remotes/publish only after the maintainer has created the external resources and explicitly authorized it.

## Good first contributions

Suitable starter work includes improving recorded fixtures, adding failure diagnostics, clarifying documentation, and
adding tests for an already-supported ecosystem. New providers and ecosystems require the adapter guide, a compatibility
review, security review, and roadmap/decision-log entry before implementation.
