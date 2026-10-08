# CLI specification

The planned command is `fundgraph`.

```text
fundgraph analyze [PATH] [--format text|json] [--offline] [--strict]
fundgraph version
fundgraph --help
```

`PATH` defaults to the current directory. `--offline` prohibits network access. `--strict` fails on unsupported or malformed required inputs; default mode returns partial results with explicit diagnostics. Exit codes will distinguish success, partial analysis, invalid input, and internal failure.

Until Phase 2, these are specifications, not available commands; README examples must be marked accordingly or updated when implemented.

