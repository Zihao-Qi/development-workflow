# Review playbook

Use for a requested code review or the final review of an implemented change.

## Scope

A review-only request produces findings and does not authorize edits or external comments. During an already authorized implementation, review your change and fix in-scope defects before handoff. Keep optional redesigns separate from defects.

## Workflow

1. Identify the requested scope and comparison base: a supplied diff, commit range, working changes, or named files. Inspect existing user changes and attribute which edits belong to the task. Do not silently review a different branch or diff.
2. Read the relevant surrounding code, callers, contracts, and tests. Trace concrete consequences at the public boundary, including compatibility, error handling, persistence, or concurrency when relevant.
3. Run focused non-mutating checks when they can confirm a finding. A scratch experiment may live outside the reviewed tree when permitted. Do not edit reviewed files merely to prove a point in a review-only task.
4. Assess correctness, regression risk, retained coverage, and whether the change solves the requested problem. Apply the architecture risk checks below when relevant. Seek concrete triggers and affected behavior; avoid speculative complaints or enforcing unrelated style preferences.
5. For independent review, the worker gets the task and raw artifacts. The owner verifies each finding against the actual code, resolves disagreements with evidence, and rechecks affected behavior after fixes.

## Architecture risk checks

Use these questions during design and review, proportional to the affected area:

- Does mutable state have a clear owner, or can independent writers or copies diverge?
- Are competing paths for the same operation unnecessarily retained, inviting callers to extend different conventions?
- Can callers bypass the intended public boundary by importing internals? Where practical, enforce that boundary through exports, types, or existing build checks.
- Are repeated lists or schemas derived from one authoritative source? If derivation is impractical, can an existing check detect disagreement?

These are risk questions, not blanket redesign requirements. Tie a finding to an affected contract or concrete failure mode. Preserve intentional compatibility paths and externally used APIs unless changing them is authorized.

## Deliverable

Put actionable findings first, ordered by impact. Each finding needs a specific location, trigger or evidence, consequence, and a focused recommendation. Label uncertainty and distinguish a reproduced defect from a plausible risk. Report no actionable findings when appropriate; do not invent issues to fill a quota.

State the scope reviewed, checks performed, and limitations. Passing tests or reviewer agreement is supporting evidence, not a guarantee of correctness. In a review-only task, a complete review may legitimately report defects and untested areas without fixing them.
