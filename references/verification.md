# Verification standard

Verification must support the success criteria with observed evidence. Compilation, a worker's summary, or the existence of tests is not proof that behavior works.

## Select proportionate checks

Select checks that directly support the criteria; this is a menu, not a requirement to run every level:

1. Static checks such as formatting, linting, type checking, or compilation.
2. Focused tests covering the changed behavior.
3. Relevant package, integration, or repository tests.
4. A runtime exercise through the same interface a user or caller uses.
5. Final diff inspection for unintended changes.

Run fast, focused checks first. Expand only as the affected surface and risk justify. For measured performance claims, apply [Performance](performance.md) as well.

## Verify the contract

- Map each essential behavioral criterion to a check that observes that behavior. Static checks support structural or type claims but cannot stand in for a behavioral check. Non-code deliverables need evidence appropriate to their claims.
- Distinguish essential checks from optional additional coverage. Mark missing essential evidence as unverified and report a partial result; do not claim the whole change is complete. An unavailable optional check does not by itself block completion.
- Prefer literal expected outcomes over assertions that only confirm a helper was called.
- Re-run the original reproduction for a bug fix.
- Compare before and after behavior for a refactor.
- Exercise the public boundary and meaningful failures for a feature.
- Consider empty input, invalid input, retries, partial failure, concurrency, persistence, and compatibility only when relevant to the changed behavior.

## Runtime readiness and cleanup

Before driving an app, establish that the intended instance is usable, not merely running or listening on a port. Confirm the relevant build, initialization, migrations, authentication, and test data as needed for the scenario. Prefer observable readiness checks over fixed sleeps.

Use isolated local fixtures within the authorized scope. If required data or another precondition is missing, supply it safely or report the scenario as unverified with the reason. Do not weaken the scenario to fit the available fixtures.

Clean up only processes, instances, and scratch state created by the check, including after failed attempts. Track their identities; do not kill by process name or remove shared user state. Keep evidence outside disposable scratch state, confirm it survives cleanup, and protect secrets in retained artifacts.

## Handle failures honestly

If a check fails, determine whether the implementation, the test, or the environment is responsible. Fix in-scope defects and rerun the check. Compare with a baseline when an unrelated failure is suspected. Do not weaken the acceptance criteria or tests to obtain a pass. Do not describe a failed, skipped, inconclusive, or wrong-surface check as passing.

Use safe local substitutes when they prove the same criterion. For mocks, containers, or local stand-ins, state which claims they prove and which they cannot. List any setup supplied by the substitute that the real target will not supply; those steps remain unverified until exercised on the target. Do not treat a prepared instance as evidence that first-run setup works.

If required credentials, a service, hardware, or a tool are unavailable, complete independent checks and report the missing evidence and next action. Do not retry indefinitely without new evidence or imply that a substitute proves an unavailable integration.

Record the exact command or interaction, its result, and the behavior it proves. Keep output excerpts short and protect secrets.
