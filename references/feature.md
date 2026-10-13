# Feature playbook

Use this playbook for new behavior or an intentional change to existing behavior.

## Outcome

Deliver a focused vertical slice that fits the existing system and is proven through user-observable behavior.

## Workflow

1. Translate the request into provisional observable acceptance criteria, constraints, and non-goals. Refine the criteria after inspection without changing the user's requirements.
2. Inspect the affected subsystem and its callers when present. Identify the authoritative data shape, ownership, boundaries, and existing extension points. Apply the [architecture risk checks](review.md#architecture-risk-checks) to the proposed shape: state ownership, competing paths, bypassable boundaries, and hand-synchronized lists or schemas. For a new project, choose only the minimal structure and runtime needed for the first usable slice.
3. Resolve factual uncertainty by inspecting or running the system. Ask the user only for product choices that evidence cannot decide.
4. When multiple designs have materially different consequences, compare the smallest credible options before choosing. Record the choice and tradeoff.
5. Plan a small vertical slice that reaches real behavior. Avoid scaffolding that cannot be verified independently.
6. Identify blocking work, independent work, and shared mutable state. Parallelize only bounded work with disjoint ownership when the user and harness permit it.
7. Implement in reviewable increments that preserve a working state.
8. Add or update retained automated tests for changed behavior when a stable test boundary exists, following the project's test setup. Assert public or user-facing outcomes. Cover important failure and edge cases proportional to risk. If automated coverage is impractical, explain why and provide reproducible substitute evidence.
9. Exercise the feature on the real runtime surface when feasible, then inspect the final diff.

## Deliverable

Report what users can now do, the important design choice, the files or components affected, the verification evidence, and any intentionally deferred scope.
