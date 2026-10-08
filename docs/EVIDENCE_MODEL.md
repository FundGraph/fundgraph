# Evidence model

Evidence is an immutable observation used to explain a result. It records what was observed, where, when, and how. Examples include package metadata funding fields, a repository `FUNDING.yml`, a canonical repository field, or a public provider response.

## Confidence rules

- **High:** multiple compatible first-party declarations support the same relationship.
- **Medium:** one direct first-party declaration or compatible registry-to-repository mapping supports it.
- **Low:** indirect or stale metadata supports it.
- **Unknown:** evidence is missing, malformed, or contradictory.

Confidence is never a substitute for evidence. A report must show evidence IDs, source links or local paths, the rule that produced the relationship, and any conflicts. URLs are findings to review, not endorsements.

