# Performance evidence

Use alongside the selected task route when measuring performance, comparing options, or optimizing behavior. Establish a baseline and the intended outcome before changing code. A measurement or diagnosis request alone does not authorize optimization.

## Define the claim

State the claim to test, its metric and unit, the workload, and the interface a user or caller exercises. Inspect the existing measurement harness: what it times, counts, and excludes. Prefer project tooling over new benchmark machinery.

For a requested quick estimate, one run can suffice if output correctness and actual work are checked. Label it as a single-run estimate, not proof that one option is better. Comparative claims need evidence strong enough to distinguish the options.

## Check the measurement

1. **Correct work.** Confirm expected outputs and side effects, not just their presence. Count failures, timeouts, retries, and non-success responses. Verify that the intended work occurs inside the measured region, including awaiting asynchronous work, consuming lazy results, and including completion costs relevant to the claim. Fast rejection or a no-op is not a speedup.
2. **Fair conditions.** Use equivalent data, versions, resource budgets, build modes, and production-relevant configuration. Treat warm and cold caches explicitly. Tune each option comparably before recommending adoption; otherwise label the result as a configuration comparison and state the limitation.
3. **Repeatability.** Check machine load and competing activity with available platform tools. When noise could affect the conclusion, repeat paired measurements and alternate or interleave the sides so warmup, cache effects, and drift favor neither. Report the run count, an appropriate summary such as the median, and variation such as the range. Choose the run count proportionally; there is no fixed minimum for every task. A gap indistinguishable from run-to-run variation is not a demonstrated improvement.
4. **Bottleneck and plausibility.** Investigate what limits the measured path before attributing a speedup, predicting a ceiling, or dismissing an unchanged result. Check whether the load generator, rather than the target, saturates first. Use separate diagnostic profiling runs when instrumentation would distort reported timings. Sanity-check the result against resource bandwidth and the original share of time spent in the changed component. State when the limiter remains unknown rather than guessing.
5. **User-visible relevance.** For a microbenchmark used to justify an optimization, also check the end-to-end path with realistic data sizes and concurrency when feasible. Report the component's share of the whole; a large helper-level gain may have negligible user impact. If the real path cannot be measured, limit the claim to the observed workload.

## Report and decide

Lead with faster, slower, no measurable difference, or inconclusive for the tested workload. Give the baseline and result with units, conditions, run count, variation, observed limiter or uncertainty, and the command and artifact supporting the claim.

Missing output-correctness or actual-work checks, unfair conditions for the intended comparison, or unresolved noise make a comparative verdict inconclusive. Identify the missing evidence. Do not discard slower runs without an evidenced reason or broaden a result beyond the path measured.

For an authorized optimization, make one justified change at a time, rerun the same comparison, and retain behavior checks. Keep or revert only your own changes based on the requested target and observed evidence, not the microbenchmark alone.
