---
name: development-workflow
description: Coordinate software development with a short plan, task-specific workflows, review, and evidence of completion. Use for substantial codebase investigations, bug fixes, features, refactors, and code reviews, or when asked to organize development work. Keep simple edits lightweight; skip unrelated questions.
license: MIT; see LICENSE
---

# Development workflow

Organize the work from the requested outcome to evidence of completion. Own the result even when other workers contribute. Follow higher-priority harness instructions, applicable repository rules, and the user's explicit choices; adapt these playbooks to that scope. A workflow does not grant tools, model access, or permission for additional actions.

## Establish the task

1. Identify the requested deliverable: an answer, a plan, a review, or an implemented change. A diagnosis or review request alone does not authorize a fix. A combined request to investigate and fix authorizes both phases without another confirmation.
2. Read the applicable project instructions. Inspect repository state, including staged, unstaged, and untracked work when Git is present. Preserve unrelated files and edits. If requested work overlaps existing edits, inspect and work around them; ask only when they cannot be safely preserved. Without Git, inspect the affected files before replacing content.
3. State provisional success criteria from the request. Inspect relevant code, tests, configuration, and current behavior, then refine the criteria before implementation. Name important constraints and non-goals; do not invent product requirements.
4. Choose the route by the requested outcome and read only its reference:

| Requested outcome | Route |
| --- | --- |
| Explain, diagnose, investigate, or recommend | [Investigation](references/investigation.md) |
| Assess a diff or code without changing it | [Review](references/review.md) |
| Correct demonstrated incorrect behavior | [Bug fix](references/bug-fix.md) |
| Add or intentionally change behavior | [Feature](references/feature.md) |
| Change structure while preserving observable behavior | [Refactoring](references/refactoring.md) |

For performance measurements, comparisons, or optimization, also read [Performance](references/performance.md). It supplements the selected route; measuring a problem does not authorize a fix.

For a plan-only request, use the relevant route to investigate and propose steps, then deliver the plan. Do not proceed to implementation.

For other development work, build a short workflow from the outcome, affected area, and proof required. For example, a CI failure may use Bug fix; a performance change needs a measured baseline and target; documentation work needs accuracy and example checks. Use the closest route only if it fits. Do not add a playbook or turn an unrelated request into development work just to satisfy this router.

## Coordinate execution

For substantial work, keep a short plan in the conversation or the harness's task list. Include the intended result, affected areas, ordered steps and dependencies, material risks, and how each essential criterion will be checked. Identify the current phase and next action. Do not create a project tracking file unless useful for a long task or requested.

Use these checkpoints to move between phases:

- Investigation ends with supported findings and the relevant contract or unresolved question.
- Design ends with a chosen approach and a way to verify it; use the existing design directly when no new decision is needed.
- Implementation ends with a reviewable change and focused checks run.
- Review and verification end with findings resolved or disclosed and the requested criteria assessed.

Revisit an earlier phase when evidence invalidates a decision. Update the plan and criteria without dropping a user requirement. For mixed requests, move to the next authorized phase when its prerequisites are ready. Send concise updates at meaningful checkpoints, failures, and changes of direction. If an essential dependency is unavailable, finish independent work and report the specific remaining dependency instead of repeatedly retrying an unchanged failure.

## Work deliberately

- Prefer the smallest coherent change that satisfies the success criteria.
- Keep unrelated cleanup out of the change.
- Base decisions on repository evidence or runtime evidence. Label inferences and unresolved uncertainty.
- Preserve existing style and architecture unless changing them is part of the request.
- Use existing tests and project commands before creating new machinery.
- Do not invent commands, APIs, configuration, file paths, test results, or tool capabilities.

## Use workers when useful

Delegation is optional and follows the current harness's available tools and permission model. Use sequential execution when workers are unavailable or the task is too tightly coupled. Keep the existing model selection unless the user requests a different one.

Give each worker a concrete task, relevant inputs including the original request and later requirements, allowed files or isolated workspace, permitted actions, success criteria, and expected evidence. Pass absolute paths to this skill and applicable references, and tell the worker to read them before starting. Resolve bundled paths relative to this skill's directory, not the worker's working directory. Use disjoint ownership for editing workers.

Prefer a fresh worker for standalone follow-ups or retries, with consolidated instructions, prior findings, and the current artifact or workspace location. Reuse a worker when its pending edits, checkout, or live processes make transferring state costly. A fresh worker does not make a shared workspace safe; stop or coordinate its prior owner before assigning edits there.

For independent review, provide the task and raw artifacts without telling the reviewer what conclusion to reach. Collect results, inspect the actual changes and outputs, resolve conflicts, and verify the combined result yourself. Do not treat a worker's completion message as verification or leave workers modifying files after handoff.

## Permission boundary

Authorization already given by the user carries through the task. Proceed with normal implementation steps within that scope and the harness's permissions. Obtain additional authority only when needed for a new action such as publishing, pushing, merging, deploying, contacting people, or destructive operations. Revert only your own task edits; do not overwrite or discard existing user work. A successful check does not authorize a release.

## Review, verify, and hand off

For a change, use [Review](references/review.md) to inspect the final diff, then apply [Verification](references/verification.md). Independent review is useful for consequential or cross-cutting changes when available and permitted; self-review is a valid fallback and must not be described as independent. Re-run affected checks after fixes. For an answer, plan, or review alone, use that route's evidence requirements without imposing a change's build/test sequence.

Report the result, important choices, changed files if any, observed checks, and remaining limitations. Match the detail to the task. Be explicit about completion:

- **Complete:** the requested work and its essential verification are satisfied.
- **Partial:** useful work is done, but required work or evidence remains. Identify it, including checks that failed or could not run.
- **Blocked:** further necessary work depends on specific missing access, information, or an external change. State what would unblock it.

Optional checks that are unnecessary for the requested outcome do not prevent completion. Choose status against the actual deliverable: a supported diagnosis can be complete even if the recommended fix is unimplemented.

Adapted from [pstack](https://github.com/cursor/plugins/tree/main/pstack) by Lauren Tan. The original MIT notice is retained in [LICENSE](LICENSE).

Upstream comparison baseline: pstack 0.15.21, commit [`997ffc7fe26bdaa6478a14e7f5b8d5f9ed747102`](https://github.com/cursor/plugins/commit/997ffc7fe26bdaa6478a14e7f5b8d5f9ed747102), dated 2026-10-12. Selected guidance was incorporated; this is not a full mirror or the original adaptation revision.
