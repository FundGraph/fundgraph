# Data model

All models have a schema version and stable identifiers.

- `Project`: input root, detected ecosystems, analysis timestamp, tool version.
- `Dependency`: package reference, requested/resolved version, dependency kind, source location, parent IDs.
- `Package`: ecosystem, normalized name, version, registry URL, metadata evidence IDs.
- `Registry`: ecosystem, canonical host, package identity rules.
- `Repository`: canonical URL, host, owner/repository path, source evidence IDs.
- `FundingSource`: provider category, URL or provider identifier, display label, evidence IDs.
- `Evidence`: kind, source URL/path, observed value, retrieval time, content hash where appropriate, and parser.
- `Relationship`: typed edge between entities, rule ID, confidence, evidence IDs, and conflict status.
- `Confidence`: `high`, `medium`, `low`, or `unknown`; confidence is about support for a relationship, not a guarantee of correctness.

No model may require a person name or infer a person’s identity. Contradictions are represented as separate evidence and relationship status, never overwritten.

