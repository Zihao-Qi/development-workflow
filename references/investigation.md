# Investigation playbook

Use this playbook when the requested result is understanding, diagnosis, or a recommendation rather than a code change.

## Outcome

Produce an evidence-backed explanation that answers the user's actual question. An investigation-only request authorizes inspection and non-mutating diagnostics. For a combined request to investigate and implement, return to the next authorized phase after establishing the findings.

## Workflow

1. Restate the question as one concrete investigation target.
2. Identify the likely entry points with repository search. Do not assume names or locations.
3. Trace the relevant path from input through state and decision points to observable output or side effects.
4. Inspect tests, types, configuration, history, or documentation when they can confirm the contract or motivation.
5. Test uncertain behavioral claims with a safe read-only experiment when feasible.
6. Separate findings into:
   - Observed facts supported by code, output, or documentation.
   - Inferences that connect those facts.
   - Unknowns that available evidence cannot resolve.
7. If the user requested a decision, compare the material tradeoffs and give a clear recommendation.

## Deliverable

Lead with the answer. Then explain the main concepts, execution flow, important file locations, and practical gotchas. Cite file paths, symbols, commands, or source links close to the claims they support.

Check that the evidence supports the answer and mark uncertainty. A factual explanation does not require a build or a full test run. If the request is only an investigation, describe proposed changes as recommendations. If implementation is already requested, carry the findings into that phase without asking for the same authorization again.
