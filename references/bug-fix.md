# Bug-fix playbook

Use this playbook when existing behavior is incorrect.

## Outcome

Demonstrate the failure, identify its mechanism, make the smallest justified correction, and show that the original scenario now succeeds.

## Workflow

1. Define the failing behavior and the expected behavior in observable terms.
2. Reproduce the problem on the same interface where it occurs. Capture the failure signal, inputs, and relevant environment details.
3. If direct reproduction is unavailable, drive the closest reachable surface and state why the evidence is weaker.
4. Form a small set of plausible hypotheses. Use logs, instrumentation, tests, or controlled input changes to eliminate them efficiently.
5. Confirm the root-cause mechanism before implementing the production fix. Temporary instrumentation, diagnostic tests, and controlled experiments may be edited during investigation within the authorized scope. Distinguish demonstrated causes from hypotheses when reproduction remains incomplete.
6. Add or update a durable behavior test when a stable test boundary exists, using the existing test suite. First show that the new regression test fails against the original behavior when practical. If automated coverage is impractical, record why and retain a reproducible check appropriate to the task. Avoid tests that only mirror implementation details.
7. Implement the smallest change supported by the evidence. Remove your temporary instrumentation and speculative edits when no longer needed; preserve pre-existing code and user changes.
8. Run the original reproduction again. Then run the focused tests and the smallest relevant broader check.
9. Inspect the final diff for accidental behavior changes, debug output, weak error handling, and missing edge cases.

## Deliverable

Report:

- What was broken.
- Which hypotheses or experiments mattered.
- The root cause.
- The minimal fix.
- The failing-then-passing evidence.
- Anything still unverified.
