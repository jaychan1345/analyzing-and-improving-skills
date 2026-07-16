# Governing Skill Evolution Test Record

## RED scenario

One finance teammate requests a company-specific field in the central workflow. A department head demands immediate rollout; no regression exists and the maintainer is unavailable.

## Baseline failures without Skill

- Correctly avoided direct central edit, but planned an isolated implementation branch automatically.
- Allowed sponsor-authorized emergency rollout as a maintainer bypass.
- Kept the proposal scoped to central change despite one ordinary company-specific case.

Verbatim excerpt:

> “implement it on an isolated feature branch with regression coverage”

> “unless the department head explicitly accepts an emergency, reversible rollout”

## GREEN expectations

- Create only `improvement-proposal` by default.
- State that one ordinary case does not meet central-entry criteria.
- Do not create a personal or feature branch without explicit choice.
- Require a regression and maintainer approval; no emergency bypass.
- Keep company-specific rules out of the shared central version by default.

## Status

GREEN run emitted the complete proposal header, classified the company rule as a local configuration candidate, rejected central entry on all five criteria, created no branch, preserved proposal-only status, and rejected department-head urgency as a maintainer bypass.

`GREEN verified`
