# Branch Policy

## Central version

- One maintained canonical suite.
- Accepts proposals from other users.
- Changes only through approved proposal, regression, evaluation, and release decision.

## Personal branch

Create only after an explicit user choice. Record:

- distinct Skill `name` with owner marker;
- central source version;
- owner and intended users;
- personal rules and scope;
- compatibility and divergence risks;
- personal test results.

Do not present a personal branch as the central version. To merge back, submit the difference, evidence from distinct cases, regression results, and a new central proposal.

## Proposal-only default

When the user has not selected a branch target, create only `improvement-proposal`. Do not create a feature branch, personal branch, implementation, or release artifact automatically.
