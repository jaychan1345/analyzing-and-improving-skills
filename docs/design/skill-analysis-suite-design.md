# Skill Analysis Suite Design

## Objective

Provide a portable workflow that can analyze a single `SKILL.md` or a complete Skill package, derive a non-destructive improved version, evaluate release readiness, and govern improvements to the workflow itself.

## Boundaries

- One Skill owns one independently triggered and accepted stage.
- The orchestrator routes work and artifacts; it does not replace specialists.
- Analysis is read-only.
- Improvement never overwrites the source and stops for approval before derivation.
- Evaluation reports failed or unverified checks without changing business rules.
- Governance treats a central change and a personal customization as different decisions.

## Artifact chain

```text
task-brief
  -> analysis-brief
  -> change-plan
  -> derived Skill
  -> evaluation-report
  -> release decision

Repeated suite-level failure
  -> improvement-proposal
  -> approval and regression
  -> central release or personal branch
```

Every artifact uses a versioned header with `artifact_type`, `artifact_version`, `case_id`, `source_skill`, `generated_at`, `status`, and `owner`.

## Approval gates

1. Scope: limited single-file analysis or complete-package analysis.
2. Change: approve a concrete `change-plan` before generating a derived Skill.
3. Release: evaluate first, then install or share.
4. Process improvement: approve an `improvement-proposal` and its regression before modifying the suite.

## Central and personal evolution

A central improvement requires either evidence from at least two distinct cases or a high-risk defect, measurable benefit, bounded context cost, a failing-old/passing-new regression, and maintainer approval. Other users submit proposals by default. They maintain a personal branch only by explicit choice and with distinct names and provenance.
