# Artifact Contracts

## Common header

Every artifact begins with:

```yaml
artifact_type: task-brief | analysis-brief | change-plan | evaluation-report | improvement-proposal
artifact_version: "1.0"
case_id: stable-case-id
source_skill: source-name-or-path
generated_at: ISO-8601 timestamp
status: current-workflow-state
owner: responsible-person-or-role
```

Do not omit a field. Use `unknown` or `not-assigned` when the fact is unavailable.

## `task-brief`

Use this order:

1. User objective
2. Source inputs and locations
3. Requested stages and boundaries
4. Allowed mutations (`read-only`, `derive-new`, or approved installation). Never record source overwrite as an allowed mode.
5. Required deliverables
6. Approval roles and gates
7. Known missing dependencies and limitations
8. Planned state sequence

Separate two approval classes:

- **Workflow approvals:** scope, `change-plan`, release, and suite-improvement decisions.
- **Target-domain approvals:** finance, legal, security, or other rules that the derived Skill must enforce.

A target-domain approval requirement is an input to analysis and change planning. It does not approve the `change-plan` itself. If its approver role, evidence, timing, rejection, or timeout behavior is undefined, record `blocked-by-business-rule` until the business owner defines it.

## Handoff rules

- Pass each artifact unchanged as the next stage's primary input.
- Append evidence or a new version; do not silently rewrite an approved artifact.
- Separate confirmed facts, inferences, problems, recommendations, and decisions.
- Tie every approval to `case_id`, artifact type, artifact version, and target version.

## Final delivery summary

Use this order:

1. Outcome and current status
2. Source and derived Skill versions
3. Completed artifacts with paths
4. Evaluation verdict and evidence
5. Unverified items and limitations
6. Installation or sharing action actually performed
7. Pending approvals or next decision
