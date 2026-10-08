# CLI specification

The command is `fundgraph`.

```text
fundgraph analyze [PATH] [--format text|json] [--offline] [--strict]
fundgraph version
fundgraph --help
```

`PATH` defaults to the current directory. `--offline` prohibits network access. `--strict` fails on unsupported or malformed required inputs; default mode returns partial results with explicit diagnostics. Exit codes will distinguish success, partial analysis, invalid input, and internal failure.

Phase 2 implemented this command surface with a JSON model input contract. Phase 3 additionally supports project directories containing npm, PyPI, or Cargo manifests and lockfiles through the core discovery API. Phase 14 adds baseline Go `go.mod` discovery through the same API. JSON files and `-`/omitted stdin remain supported. Directory discovery performs no network access, and `--offline` remains explicit for forward compatibility.

Exit codes are `0` for success, `1` for partial analysis with diagnostics, `2` for usage or invalid input, and `3` for unexpected internal failures. Text output contains the compatibility analysis summary followed by a deterministic report. JSON output retains the summary fields and adds a `report` object with schema version `1.0`, stable arrays for models and relationships, relationship status counts, evidence, diagnostics, limitations, and non-executing review/inspect actions. Report actions are informational only; FundGraph never makes funding decisions or payments. Live network orchestration is exposed by the core library’s injected `NetworkClient`; the current CLI directory analyzer remains offline and does not silently enable network access.

