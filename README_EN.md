# Skill Analysis, Improvement, and Governance Suite

[简体中文](README.md) | [English](README_EN.md)

> A coordinated five-Skill suite for analyzing, improving, evaluating, orchestrating, and governing AI Skills.

This repository is not a single business Skill. It is a reusable operating system for understanding an external Skill, planning safe changes, validating a derived version, and governing continuous improvement. It is especially useful for teams that turn repeatable work into Skills, including cross-border e-commerce operations, ERP exports, finance reconciliation, and standardized reporting.

The suite follows seven principles:

- collect evidence before drawing conclusions;
- keep analysis read-only by default;
- approve an exact change plan before creating a derived version;
- preserve the source instead of overwriting it;
- distinguish static review, executed evidence, observation, and unverified claims;
- accept proposals for the central suite by default;
- create a personal branch only after explicit opt-in.

## What This Suite Solves

When a team receives a shared `SKILL.md` or a complete Skill package, it often needs answers to questions such as:

- When should the Skill trigger, and where are its boundaries?
- Which files, fields, scripts, templates, assets, and external tools does it require?
- Are its workflow, decisions, failure handling, and acceptance criteria complete?
- Which statements are direct facts, supported inferences, or unverified assumptions?
- Which requirements should be retained, changed, added, removed, or split?
- Has the exact change been approved, and is the source still intact?
- Does the derived Skill pass trigger, function, failure, regression, and portability tests?
- Should a successful improvement enter the central suite or remain a personal branch?

The five runtime Skills answer these questions through specialist stages and pass versioned artifacts from one stage to the next.

## When to Use It

Use this suite when you need to:

- decompose or audit a single `SKILL.md` without changing it;
- inspect a complete package, including `references/`, `scripts/`, and `assets/`;
- adapt an external Skill to company requirements without overwriting its source;
- split or restructure a Skill after an approved plan;
- test trigger behavior, normal paths, missing inputs, abnormal inputs, contracts, regressions, and portability;
- orchestrate a request spanning analysis, improvement, evaluation, release, installation, or governance;
- govern proposals, approvals, versions, branches, releases, and rollbacks for this suite itself;
- package repeatable ERP, finance, and reporting workflows as maintainable Skills.

Do not use the suite to invent missing business definitions, bypass approval gates, replace a one-off data task that needs no reusable process, or claim release readiness when critical tests were not run.

## The Five Runtime Skills

| Skill | Use it when | Changes the target? | Primary input | Primary artifact |
|---|---|---:|---|---|
| [`analyzing-skills`](runtime/analyzing-skills/SKILL.md) | Inspecting, explaining, auditing, reverse engineering, or decomposing | No; read-only | One `SKILL.md` or a complete package | `analysis-brief`, evidence table, missing dependencies, issue list |
| [`improving-skills`](runtime/improving-skills/SKILL.md) | Explicitly modifying, optimizing, splitting, restructuring, or deriving | Yes, but only as a non-destructive derivative | `analysis-brief`, requirements, source version | `change-plan`, classified differences, approved derived Skill |
| [`evaluating-skills`](runtime/evaluating-skills/SKILL.md) | Testing, validating, reviewing, comparing, or deciding release readiness | No by default | Target version, contracts, environment, golden samples | `evaluation-report`, test matrix, `release/revise/blocked` verdict |
| [`governing-skill-evolution`](runtime/governing-skill-evolution/SKILL.md) | Proposing, approving, versioning, branching, merging, releasing, or rolling back this suite | Governs change; does not replace implementation | Failure cases, risk, scope, regression evidence | `improvement-proposal`, approval and version records |
| [`orchestrating-skill-work`](runtime/orchestrating-skill-work/SKILL.md) | One request spans two or more stages | Depends on downstream stages | Objective, source, allowed mutations, deliverables | `task-brief`, state tracking, artifact handoffs, final summary |

Important boundaries:

- `analyzing-skills` performs read-only decomposition and never treats findings as edit authorization.
- `improving-skills` handles approved modification, restructuring, splitting, or derived versions.
- `evaluating-skills` tests triggers, normal behavior, failure paths, regression, and release readiness.
- `governing-skill-evolution` manages proposals, approvals, versions, branches, merge, release, and rollback.
- `orchestrating-skill-work` is the entry point when one request spans two or more stages.

## Routing a Request

Choose the first Skill by the requested outcome, not by isolated verbs in the prompt:

1. **Explain, inspect, audit, reverse engineer, or decompose only:** use `analyzing-skills`.
2. **Modify, optimize, split, restructure, or derive:** use `improving-skills`; obtain an evidence-based analysis first if none exists.
3. **Test, validate, compare, review, or decide release readiness:** use `evaluating-skills`.
4. **Change this analysis suite itself:** use `governing-skill-evolution`.
5. **Request two or more stages:** start with `orchestrating-skill-work`.

Examples:

| Request | First Skill | Why |
|---|---|---|
| “Explain the risks before deciding whether this Skill can ship.” | `evaluating-skills` | The risk review supports one evaluation outcome. |
| “Fully decompose this Skill, then create and test a company version.” | `orchestrating-skill-work` | The request needs separate analysis, improvement, and evaluation artifacts. |
| “Improve the approval rules in this suite.” | `governing-skill-evolution` | The target is the suite itself. |
| “Improve an Amazon inventory Skill.” | `improving-skills` | The target is an external business Skill. |

See [`routing-rules.md`](runtime/orchestrating-skill-work/references/routing-rules.md) for the complete routing contract.

## End-to-End Workflow

A multi-stage case uses this primary state sequence:

```text
received
  → source-checked
  → analyzed
  → awaiting-change-approval
  → derived
  → evaluating
  → awaiting-release-approval
  → released
```

### 1. Establish scope

The orchestrator creates a `task-brief` that records the objective, source locations, requested stages, allowed mutations, required deliverables, approval roles, missing dependencies, limitations, and planned state sequence.

Allowed mutations are `read-only`, `derive-new`, or installation of an evaluated version. Source overwrite is not an allowed mode. A request to overwrite must become a new name, new version, or explicitly selected personal branch.

### 2. Produce an evidence-based analysis

Inventory the actual files and classify each reference as `present`, `missing`, `external`, or `unverified`. Then distinguish:

- `FACT`: directly supported by source content;
- `INFERENCE`: derived from facts with uncertainty stated;
- `MISSING`: referenced but unavailable;
- `ISSUE`: a gap or conflict;
- `OPPORTUNITY`: an improvement candidate, not current behavior.

A single `SKILL.md` supports file-level conclusions only. It cannot support a complete package audit when linked files are unavailable.

### 3. Plan the change

Classify each requirement as retained, changed, added, removed, or split. The `change-plan` defines the target name and architecture, affected files, migration, rollback, failure behavior, and regression tests. It then stops at `awaiting-change-approval`.

### 4. Derive only after approval

Approval must identify the current `case_id`, artifact type, artifact version, target name, and target version. General agreement from an earlier discussion is not approval for a new plan. The source remains unchanged.

### 5. Evaluate reproducibly

The test matrix covers eight types:

- `trigger`;
- `function`;
- `missing`;
- `abnormal`;
- `contract`;
- `repeatability`;
- `regression`;
- `portability`.

Each case records input, expected result, actual result, evidence, and status. A critical `not-run`, missing required dependency, or failed critical regression prevents a `release` verdict.

### 6. Release or return to the correct stage

- Missing source or dependency → analysis, status `incomplete`.
- Conflicting business rule → improvement, status `blocked-by-business-rule`.
- Trigger, contract, regression, or portability failure → evaluation, status `evaluation-failed`.
- Account, permission, secret, or production boundary → status `blocked-by-permission`.
- Passing evidence plus explicit release approval → installation or release.

See [`artifact-contracts.md`](runtime/orchestrating-skill-work/references/artifact-contracts.md) for artifact headers and handoff rules.

## Approval-Gated Evolution

The suite separates two approval classes.

**Workflow approvals** cover scope, the current `change-plan`, release or installation, and improvements to this suite.

**Target-domain approvals** cover finance, legal, security, or other rules that a derived Skill must enforce. A domain approval is an input to analysis and change planning. It does not approve the `change-plan` itself.

The central improvement lifecycle is:

```text
observed
  → proposed
  → under-review
  → approved
  → implemented
  → evaluated
  → released
```

Rejected proposals retain a reason. Missing evidence or unavailable authority leaves a proposal `proposed` or `blocked`; urgency does not silently convert it into approval.

A central change requires all of the following:

1. The issue appears in at least two distinct cases or is a high-risk defect.
2. The change measurably reduces omissions, false decisions, unsafe behavior, or repeated work.
3. It does not impose unjustified context cost on all users.
4. At least one regression fails on the old version and passes on the candidate.
5. A designated maintainer approves the exact proposal and target version.

See [`improvement-protocol.md`](runtime/governing-skill-evolution/references/improvement-protocol.md).

## Central Version and Personal Branches

The central suite has one maintained canonical version. It accepts proposals from other users, but changes only through an approved proposal, regression, evaluation, and release decision.

The central suite accepts improvement proposals by default. When no branch target has been selected, the system creates only an `improvement-proposal`; it does not automatically create a feature branch, personal branch, implementation, or release artifact.

A personal branch exists only after explicit opt-in. It must record:

- a distinct Skill `name` with an owner marker;
- the central source version;
- owner and intended users;
- personal rules and scope;
- compatibility and divergence risks;
- personal test results.

A personal branch does not represent the central version and does not automatically overwrite or synchronize back to it. Merging back requires the difference, evidence from distinct cases, regression results, and a new central proposal.

See [`branch-policy.md`](runtime/governing-skill-evolution/references/branch-policy.md).

## Cross-Border E-Commerce Examples

The following examples map common work to the suite without defining company-specific fields or thresholds. All fields, thresholds, formulas, and approval roles are illustrative; the user or business owner supplies the authoritative business definition.

| Scenario | Recommended flow | Key inputs | Main artifacts |
|---|---|---|---|
| ERP sales, inventory, and advertising spreadsheet workflow | Analyze → propose changes → implement after approval → evaluate | Source Skill, field definitions, sample sheets, business definitions | Analysis brief, derived Skill, evaluation report |
| Platform settlement statement to standard finance statement | Analyze → review risks → implement after approval → evaluate | Statements, field mapping, currency and period rules, output template | Finance-processing Skill, exception rules, standard statement |
| Company adaptation of an external Skill | Read-only analysis → difference table → improvement proposal | Complete Skill package, dependencies, company rules | Evidence table, gap list, change plan |

### ERP operations workflow

Validate date, marketplace, currency, SKU/ASIN links, duplicates, cancellations, returns, and inbound inventory behavior. Require traceability from output metrics to source columns. Company-specific alert thresholds normally belong in configuration or a personal/business derivative, not the central suite.

### Finance reconciliation workflow

Preserve original inputs and define currency, exchange-rate source, tax, fee, and accounting-period rules. Unmatched transactions must be reported instead of silently dropped. If the responsible business owner has not defined the financial rule or golden sample, use `blocked-by-business-rule` or `blocked`; do not invent an answer.

### External Skill adaptation

First establish whether the team received one `SKILL.md` or a complete package. Inventory missing references, scripts, assets, and templates. Produce the analysis and classified difference table, request approval for the exact plan, create a derived name, and evaluate before installation or sharing.

## Repository Layout

```text
analyzing-and-improving-skills/
├── README.md                         # Chinese primary guide
├── README_EN.md                      # English guide
├── INSTALL.md                        # Installation guide
├── runtime/                          # Five installable runtime Skills
│   ├── analyzing-skills/
│   ├── improving-skills/
│   ├── evaluating-skills/
│   ├── governing-skill-evolution/
│   └── orchestrating-skill-work/
├── governance/                       # Tests and release records; not runtime context
│   ├── tests/
│   ├── samples/
│   └── release/
└── docs/                             # Architecture, designs, and plans
```

Each runtime Skill includes its own `SKILL.md`, `agents/openai.yaml`, and references. V1 has no runtime `scripts/` or `assets/`.

## Quick Installation

Copy each direct child directory under `runtime/` into the personal Codex Skill directory:

```text
~/.codex/skills/
```

Windows PowerShell:

```powershell
$target = Join-Path $HOME '.codex\skills'
New-Item -ItemType Directory -Force -Path $target | Out-Null
Get-ChildItem '.\runtime' -Directory | ForEach-Object {
    Copy-Item $_.FullName -Destination $target -Recurse -Force
}
```

macOS / Linux:

```bash
mkdir -p ~/.codex/skills
cp -R runtime/* ~/.codex/skills/
```

Install only the five children of `runtime/`. The `governance/` directory contains maintenance and test evidence and must not be installed as everyday runtime context. Restart Codex if the Skills are not discovered immediately. See [`INSTALL.md`](INSTALL.md) for the complete installation and update policy.

## First Use

Read-only decomposition:

```text
Use analyzing-skills to perform a read-only decomposition of the provided Skill.
Do not modify the source. Separate facts, inferences, missing items, issues, and opportunities.
Inspect every reference to references, scripts, and assets, then produce a versioned analysis-brief.
```

Analysis, improvement, and evaluation:

```text
Use orchestrating-skill-work to coordinate analysis, improvement, and evaluation.
Create a task-brief first. After the analysis-brief, create a change-plan and stop for approval.
Do not create a derived version until I approve that exact plan. Preserve the source.
```

Improving this suite:

```text
Use governing-skill-evolution to create an improvement-proposal for this workflow problem.
Default to proposal-only; do not implement automatically. State when evidence comes from one ordinary case.
```

## Prompt Examples

| Goal | Example prompt |
|---|---|
| Analyze one file | “Decompose this `SKILL.md` read-only and list what cannot be verified at package level.” |
| Audit a complete package | “Audit the entire Skill directory and build a file tree and reference-integrity table.” |
| Classify requirements | “Use the `analysis-brief` to classify each new requirement as retain, change, add, remove, or split.” |
| Plan a derivative | “Create a `change-plan` with a new name, preserve the source, and stop for my approval.” |
| Test triggering | “Test positive, near-boundary, and negative trigger prompts and retain actual evidence.” |
| Review for release | “Cover all eight test types and return one `release`, `revise`, or `blocked` verdict.” |
| Select a personal branch | “I explicitly choose a personal branch; record source version, owner, rules, and compatibility risks.” |
| Propose a central change | “Do not edit the central suite; submit an improvement proposal with a regression case.” |

## Artifacts and Evidence

Every standard artifact starts with:

```yaml
artifact_type: task-brief | analysis-brief | change-plan | evaluation-report | improvement-proposal
artifact_version: "1.0"
case_id: stable-case-id
source_skill: source-name-or-path
generated_at: ISO-8601 timestamp
status: current-workflow-state
owner: responsible-person-or-role
```

Use `unknown` or `not-assigned` for unavailable facts; do not omit fields or replace missing evidence with a precise-looking guess.

| Artifact | Producer | Minimum handoff requirement |
|---|---|---|
| `task-brief` | Orchestrator | Scope, source, allowed mutations, deliverables, approvals, and limitations |
| `analysis-brief` | Analyzer | Evidence levels, references, missing items, and boundaries |
| `change-plan` | Improver | Classified changes, target, affected files, migration, rollback, and regression |
| `evaluation-report` | Evaluator | Environment, eight test types, expected/actual/evidence, and one verdict |
| `improvement-proposal` | Governor | Problem, evidence range, risk, context cost, and regression case |

Pass an approved artifact unchanged as the next stage's primary input. Append evidence or create a new version instead of silently rewriting an approved artifact.

## Evaluation, Release, and Rollback

Test case statuses are `passed`, `failed`, `blocked`, and `not-run`.

Release verdicts are:

- `release`: all critical cases pass; accepted non-critical limitations are explicit;
- `revise`: evidence shows fixable trigger, behavior, contract, or compatibility failures;
- `blocked`: correctness cannot be established because a required dependency, permission, business rule, or golden sample is unavailable.

Critical failures include ambiguous source or target versions, missing required files or tools, required script failure, unintended source mutation, bypassable approval gates, incomparable expected and actual results, and failed critical trigger or regression cases.

Use [`release-checklist.md`](governance/release/release-checklist.md) before release. The current release record is [`manifest.md`](governance/release/manifest.md). Rollback restores a known central version but retains the failed case and regression evidence.

## Troubleshooting

### I received only one `SKILL.md`. Can I still analyze it?

Yes, but only at file level. Mark referenced but unavailable files as `missing` or `unverified`; do not claim a complete package audit.

### Why not edit immediately after finding an obvious problem?

Analysis authorization is not edit authorization. The exact difference, target name, risks, migration, rollback, and regression must be visible in a `change-plan` before approval.

### Does “just change it” count as approval?

No. Create the current plan first, then obtain approval tied to its `case_id`, artifact version, and target version.

### Can this suite overwrite the source Skill?

No. Create a new name, new version, or explicitly selected personal branch.

### Should a company-specific rule enter the central suite?

Usually not from one ordinary case. Keep it as a proposal, configuration candidate, business derivative, or personal branch unless it meets central-entry criteria.

### Does a strong static review count as an executed test?

No. Static, executed, observed, and unverified evidence remain separate. A critical test that was not run prevents release.

### Why is `governance/` excluded from installation?

It contains tests, samples, and release evidence rather than everyday runtime instructions. Installing it would add irrelevant context and could mix maintenance policy into business tasks.

### Do other users' changes update the central suite automatically?

No. They submit proposals. Central updates require evidence, regressions, maintainer approval, evaluation, and a release decision.

### Can a personal branch reuse the central Skill name?

No. It must use a distinct owner-marked name and retain provenance.

### Where should a failed evaluation return?

Incomplete sources return to analysis; behavior or implementation defects return to improvement; permission failures remain blocked. Do not bypass failure and install anyway.

## Contributing and Maintenance

For a business Skill improvement:

1. Record the source version and provide an `analysis-brief`.
2. State the requirement source and scope.
3. Classify retained, changed, added, removed, and split content.
4. Define failure behavior and regression cases.
5. Obtain approval for the exact `change-plan`.
6. Create a non-destructive derivative.
7. Provide complete evaluation evidence.

For a central suite improvement:

1. Record a reproducible failure symptom.
2. State case count, risk, and context cost.
3. Create an `improvement-proposal`.
4. Define a regression that fails on the old version and passes on the candidate.
5. Obtain maintainer approval for the exact proposal and target version.
6. Complete implementation, evaluation, and release checks.
7. Retain the previous central version for rollback.

Before sharing the repository or ZIP, remove local test output, business data, account identifiers, secrets, and machine-specific paths.

## Release Status

Current release candidate: `1.0.0` dated 2026-07-16.

- Runtime Skills: 5
- Structural validation: passed
- Forward testing: passed
- Integration testing: passed
- Source overwrite: prohibited
- Central change default: proposal-only
- Personal branch: explicit opt-in

See [`governance/release/manifest.md`](governance/release/manifest.md) for the release record and [`INSTALL.md`](INSTALL.md) before installation or team distribution.
