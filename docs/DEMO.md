# Demo plan

The v0.1 demo uses the synthetic fixture project at `fundgraph-core/test/fixtures/npm-workspace` and shows:

1. dependency discovery from local files;
2. package-to-repository mapping;
3. funding source declarations;
4. evidence IDs and confidence;
5. a contradictory or missing-data warning; and
6. deterministic text and JSON output.

From `fundgraph-cli`, run:

```text
node dist/main.js analyze ../fundgraph-core/test/fixtures/npm-workspace --format text --offline
node dist/main.js analyze ../fundgraph-core/test/fixtures/npm-workspace --format json --offline
```

The CLI performs local discovery only. Registry and funding payload parsing is exercised by the core integration suite using recorded fixtures, not by hidden live requests.

The demo must never imply that FundGraph verified a person, guarantees a funding endpoint, or executed a payment.

