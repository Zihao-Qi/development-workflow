# Refactoring playbook

Use this playbook when structure should change while observable behavior remains the same.

## Outcome

Improve the code's shape without changing its contract, and prove behavioral equivalence at a meaningful boundary.

## Workflow

1. State the behavior that must remain unchanged. Inventory affected callers and contracts before edits, including exports, configuration references, registries, and dynamically selected consumers when relevant. Identify compatibility constraints; do not assume all consumers live in the repository.
2. Pin that contract with an existing test, a characterization test, a snapshot, or an equivalence harness before moving structure. A type check alone is not a behavior contract.
3. Describe the structural problem and the target shape. State how the result reduces branching, invalid states, duplication, coupling, or reader effort.
4. Keep discovered bugs and new features separate. Reclassify them instead of hiding behavior changes inside the refactor.
5. Remove confirmed dead or redundant structure before adding abstraction.
6. Change the structure in small increments and run the pinned behavior check after each meaningful step.
7. When replacing an internal API, update the inventoried callers and search again for remaining references. Remove the obsolete path only when its consumers have migrated and the compatibility contract allows removal. Preserve externally used contracts unless changing them is part of the request.
8. Run focused tests, the relevant broader checks, and a real behavior or equivalence check when feasible.
9. Inspect the diff. If the result adds indirection without a concrete reduction in complexity, simplify or revert only your refactoring edits. Preserve existing user work.

## Deliverable

Report the preserved contract, the old and new structural shapes, the evidence of equivalence, and the concrete reduction in complexity.
