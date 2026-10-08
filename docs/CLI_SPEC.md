# CLI specification

The planned command is `fundgraph`.

```text
fundgraph analyze [PATH] [--format text|json] [--offline] [--strict]
fundgraph version
fundgraph --help
```

`PATH` defaults to the current directory. `--offline` prohibits network access. `--strict` fails on unsupported or malformed required inputs; default mode returns partial results with explicit diagnostics. Exit codes will distinguish success, partial analysis, invalid input, and internal failure.

Phase 2 implements this command surface with a deliberately narrow JSON model input contract: `PATH` is a JSON file, or `-`/omitted for stdin, containing an array of versioned FundGraph models or `{ "models": [...] }`. Directories and dependency manifests are not analyzed until Phase 3. Phase 2 performs no network access, and `--offline` remains explicit for forward compatibility.

Exit codes are `0` for success, `1` for partial analysis with diagnostics, `2` for usage or invalid input, and `3` for unexpected internal failures. Text and JSON output contain stable model counts and diagnostics.

