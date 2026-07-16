# Routing Rules

## Stage selection

| Observable request scope | First Skill |
|---|---|
| Only explain, inspect, audit, reverse engineer, or decompose | `analyzing-skills` |
| Explicitly modify, optimize, split, restructure, or derive | `improving-skills` |
| Test, validate, compare, review, or decide release readiness | `evaluating-skills` |
| Propose, approve, version, branch, merge, release, or roll back this suite | `governing-skill-evolution` |
| Two or more stages in one request | `orchestrating-skill-work` |

## Boundaries

- Count requested outcomes, not verbs. “Analyze risks before testing” is evaluation unless it also requests a standalone decomposition artifact.
- Route target-Skill improvements to `improving-skills`; route improvements to this analysis system to `governing-skill-evolution`.
- Do not invoke the orchestrator for a single specialist stage.
- If a required specialist is unavailable, stop with `blocked-by-permission` or `incomplete`; do not simulate completion invisibly.

## State transitions

| Current | Evidence required for next state | Next |
|---|---|---|
| `received` | source location and scope recorded | `source-checked` |
| `source-checked` | completed `analysis-brief` | `analyzed` |
| `analyzed` | change requested and `change-plan` issued | `awaiting-change-approval` |
| `awaiting-change-approval` | explicit approval tied to the plan | `derived` |
| `derived` | evaluation started with target version | `evaluating` |
| `evaluating` | passing report with limitations | `awaiting-release-approval` |
| `awaiting-release-approval` | explicit installation or release decision | `released` |

## Failure routing

- Missing source or dependency → analysis, status `incomplete`.
- Ambiguous or conflicting business rule → improvement, status `blocked-by-business-rule`.
- Trigger, contract, regression, or portability failure → evaluation, status `evaluation-failed`.
- Account, production, permission, or secret boundary → status `blocked-by-permission`.
