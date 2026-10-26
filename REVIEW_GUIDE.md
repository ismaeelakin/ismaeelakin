# Review selected work

Choose a project by the question you want to investigate. These routes use the checked-in examples and tests; no private data or paid services are needed.

## Use a complete browser product

[Open Rowcraft](https://ismaeelakin.github.io/rowcraft/) and check the example file. It should report **10 records, seven ready and three needing review**. Require the email column: ready records should drop to six. Inspect a flagged record, then download the CSV and JSON report.

Repeat the workflow with your own UTF-8 file. Compare [the parser](https://github.com/ismaeelakin/rowcraft/blob/main/src/csv.ts), [checking rules](https://github.com/ismaeelakin/rowcraft/blob/main/src/quality.ts) and [export tests](https://github.com/ismaeelakin/rowcraft/blob/main/test/export.test.ts). The [benchmark procedure](https://github.com/ismaeelakin/rowcraft/blob/main/docs/PERFORMANCE.md) measures parsing and checking separately from browser interaction.

Question to investigate: what happens to a valid duplicate when an earlier record with the same key is rejected?

## Inspect Rust and C numerical work

Open [Latency Atlas](https://github.com/ismaeelakin/latency-atlas). Run the sample `0, 1, 2, 4, 8, 16, 32, 100` through the CLI. Its p50 bound is `[4,7]`; p95 and p99 are `[64,100]`. Those are bounds, not exact-percentile claims.

Read the [rank arithmetic](https://github.com/ismaeelakin/latency-atlas/blob/main/docs/DESIGN.md), then run the documented Rust/C/Python conformance procedure. The Python harness checks exact sorted ranks independently of either implementation.

Question to investigate: how does the C implementation avoid overflowing `count * basis_points` without a nonstandard integer type?

## Follow real webhook delivery

Clone [Dispatch Ledger](https://github.com/ismaeelakin/dispatch-ledger), install locked development dependencies with `npm ci`, and run `npm run demo`. The local demo uses synthetic events and real HTTP receivers.

Inspect `invoice.paid`: its receiver returns 503 twice, then 204. Publish the same idempotency key twice, then try a changed payload with that key. Compare the original-event response with the conflict response. Switch tenant and inspect the isolated view.

Start with [the store](https://github.com/ismaeelakin/dispatch-ledger/blob/main/src/store.ts), [SQL constraints](https://github.com/ismaeelakin/dispatch-ledger/blob/main/migrations/001_initial.sql) and [worker tests](https://github.com/ismaeelakin/dispatch-ledger/blob/main/test/worker.test.ts).

Question to investigate: which database writes must commit together, and which work deliberately happens outside the transaction?

## Exercise a durable queue

Clone [RelayBox](https://github.com/ismaeelakin/relaybox) and run `python -m relaybox.server`. Enqueue the example JSON and acknowledge it. Enqueue another job and simulate failures, allowing the documented retry delays. Replay the dead letter.

Read [the delivery semantics](https://github.com/ismaeelakin/relaybox#delivery-semantics) and [stale-token tests](https://github.com/ismaeelakin/relaybox/blob/main/tests/test_store.py).

Question to investigate: why can a lease token protect queue state without guaranteeing exactly-once external effects?

## Review smaller JavaScript work

- [Guess My Number](https://ismaeelakin.github.io/Guess_My_Number_JS-Project/): input validation, state transitions, keyboard interaction and round reset.
- [Array exercises](https://ismaeelakin.github.io/js-fundamentals/): enter `3, 1, 3, -2`, then compare numeric sorting and duplicate removal.
- [Loop Trace](https://ismaeelakin.github.io/fundamental_js_part_2/): trace ascending and descending integer loops, inspect exact totals and test the iteration guard.

These are learning applications with smaller scope. The four pinned projects contain the main design and testing material.
