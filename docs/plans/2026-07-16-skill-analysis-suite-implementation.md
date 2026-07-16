# Skill Analysis Suite Implementation Plan

> **For agentic workers:** Execute each task in order. Complete RED, GREEN, REFACTOR, and validation for one Skill before starting the next.

**Goal:** Build, test, install, package, and publish five coordinated Skills for analyzing, improving, evaluating, orchestrating, and governing Skill evolution.

**Architecture:** Keep one independently triggered Skill per workflow stage. Exchange versioned Markdown artifacts between stages; keep governance tests outside runtime Skill context. Use references for contracts and detailed rules, with no V1 scripts or assets.

**Tech Stack:** Markdown, YAML, Codex Skill Creator validation scripts, Git, GitHub CLI, PowerShell packaging.

## Global Constraints

- Preserve every source Skill; optimization creates a new name or explicit personal branch.
- Keep facts, inferences, issues, recommendations, and decisions separate.
- Require approval before deriving a Skill, releasing it, or changing the central suite.
- Allow other users to submit proposals by default; create a personal branch only after explicit selection.
- Do not put account data, secrets, local absolute paths, or business datasets in the share package.
- Create no `scripts/` or `assets/` in V1.
- Validate and forward-test each Skill before moving to the next.

---

### Task 1: Repository contracts and test fixtures

**Files:**
- Create: `README.md`
- Create: `INSTALL.md`
- Create: `docs/design/skill-analysis-suite-design.md`
- Create: `governance/tests/trigger-cases.md`
- Create: `governance/samples/incomplete-skill/SKILL.md`
- Create: `governance/release/release-checklist.md`

**Produces:** A public repository shell, a synthetic incomplete Skill fixture, and the acceptance contract used by all later tasks.

- [ ] Create the repository documentation without machine-specific paths.
- [ ] Create a deliberately incomplete fixture that references a missing file.
- [ ] Record the five routing intents and adjacent negative-trigger cases.
- [ ] Run `rg -n "C:\\\\Users|gho_|api[_-]?key|password" .` and expect no sensitive matches outside documentation examples.

### Task 2: `orchestrating-skill-work`

**Files:**
- Create: `runtime/orchestrating-skill-work/SKILL.md`
- Create: `runtime/orchestrating-skill-work/agents/openai.yaml`
- Create: `runtime/orchestrating-skill-work/references/routing-rules.md`
- Create: `runtime/orchestrating-skill-work/references/artifact-contracts.md`
- Create: `governance/tests/orchestrating-skill-work.md`

**Consumes:** A request spanning at least two workflow stages.

**Produces:** `task-brief`, state transitions, routed stage artifacts, and a final delivery summary.

- [ ] Run a fresh baseline scenario without this Skill and record whether the agent performs specialist work itself, skips approval, or loses artifact boundaries.
- [ ] Initialize the Skill with Skill Creator.
- [ ] Implement only routing, state management, approvals, and artifact handoff.
- [ ] Re-run the same scenario with the Skill and verify it delegates stage work and preserves approval gates.
- [ ] Run Skill Creator `quick_validate.py`; expect `Skill is valid!`.

### Task 3: `analyzing-skills`

**Files:**
- Create: `runtime/analyzing-skills/SKILL.md`
- Create: `runtime/analyzing-skills/agents/openai.yaml`
- Create: `runtime/analyzing-skills/references/analysis-framework.md`
- Create: `runtime/analyzing-skills/references/evidence-rules.md`
- Create: `runtime/analyzing-skills/references/analysis-brief-template.md`
- Create: `governance/tests/analyzing-skills.md`

**Consumes:** One `SKILL.md` or a complete Skill directory.

**Produces:** Evidence-backed `analysis-brief` without modifying the source.

- [ ] Run the incomplete fixture without this Skill and record guessed dependencies, mixed evidence, or missing scope limits.
- [ ] Initialize and implement the Skill and three references.
- [ ] Re-run the fixture with the Skill; require explicit missing-dependency and unverified labels.
- [ ] Verify single-file and complete-package scope behavior.
- [ ] Run `quick_validate.py`; expect `Skill is valid!`.

### Task 4: `improving-skills`

**Files:**
- Create: `runtime/improving-skills/SKILL.md`
- Create: `runtime/improving-skills/agents/openai.yaml`
- Create: `runtime/improving-skills/references/change-classification.md`
- Create: `runtime/improving-skills/references/architecture-decisions.md`
- Create: `runtime/improving-skills/references/change-plan-template.md`
- Create: `governance/tests/improving-skills.md`

**Consumes:** `analysis-brief` plus new requirements.

**Produces:** An approval-gated `change-plan` and, after approval, a newly named derived Skill.

- [ ] Run a baseline optimization request with overwrite pressure and record whether the agent edits the original or bypasses approval.
- [ ] Initialize and implement the Skill and three references.
- [ ] Re-run the scenario; require preserve/modify/add/delete/split classification and an explicit approval stop.
- [ ] Verify the derived Skill uses a new name and records source provenance.
- [ ] Run `quick_validate.py`; expect `Skill is valid!`.

### Task 5: `evaluating-skills`

**Files:**
- Create: `runtime/evaluating-skills/SKILL.md`
- Create: `runtime/evaluating-skills/agents/openai.yaml`
- Create: `runtime/evaluating-skills/references/test-matrix.md`
- Create: `runtime/evaluating-skills/references/evaluation-rubric.md`
- Create: `runtime/evaluating-skills/references/evaluation-report-template.md`
- Create: `governance/tests/evaluating-skills.md`

**Consumes:** A source or derived Skill, expected contracts, and test artifacts.

**Produces:** Evidence-backed `evaluation-report` with release, revise, or blocked verdict.

- [ ] Run a baseline release-readiness request with missing scripts and record whether the agent claims success without execution.
- [ ] Initialize and implement the Skill and three references.
- [ ] Re-run the scenario; require trigger, normal, missing, abnormal, contract, repeatability, regression, and portability coverage.
- [ ] Verify an unrun script blocks release and remains listed as unverified.
- [ ] Run `quick_validate.py`; expect `Skill is valid!`.

### Task 6: `governing-skill-evolution`

**Files:**
- Create: `runtime/governing-skill-evolution/SKILL.md`
- Create: `runtime/governing-skill-evolution/agents/openai.yaml`
- Create: `runtime/governing-skill-evolution/references/improvement-protocol.md`
- Create: `runtime/governing-skill-evolution/references/branch-policy.md`
- Create: `runtime/governing-skill-evolution/references/improvement-proposal-template.md`
- Create: `governance/tests/governing-skill-evolution.md`

**Consumes:** Repeated failure evidence or a high-risk defect in this suite.

**Produces:** `improvement-proposal`, central-version or personal-branch decision, and regression obligations.

- [ ] Run a baseline single-case customization request and record whether it is merged into the central flow.
- [ ] Initialize and implement the Skill and three references.
- [ ] Re-run the scenario; require proposal-only default and explicit opt-in for a personal branch.
- [ ] Verify central changes require two distinct cases or a high-risk defect, regression, and maintainer approval.
- [ ] Run `quick_validate.py`; expect `Skill is valid!`.

### Task 7: Integration, installation, packaging, and publication

**Files:**
- Create: `governance/tests/integration-results.md`
- Create: `governance/release/manifest.md`
- Create outside repository: `skill-analysis-suite.zip`
- Install: `%USERPROFILE%/.codex/skills/{five-skill-names}`

**Consumes:** Five individually validated Skills.

**Produces:** Installed personal Skills, a portable ZIP, a Git branch, commit, push, and draft pull request.

- [ ] Validate all five folders with `quick_validate.py`.
- [ ] Check frontmatter descriptions for five distinct positive triggers and adjacent negative boundaries.
- [ ] Run an end-to-end synthetic case from analysis through release decision and record evidence.
- [ ] Scan the share tree for secrets and local absolute paths; expect zero findings.
- [ ] Copy only `runtime/*` to the personal global Skill directory and compare file hashes.
- [ ] Compress the repository runtime and governance materials into the local ZIP.
- [ ] Stage only intended repository files, commit on `agent/initial-skill-suite`, and push.
- [ ] Open a draft pull request to the remote default branch and report branch, commit, checks, and PR URL.

## Self-Review Result

- Every design requirement maps to a task above.
- No implementation step permits overwriting a source Skill.
- Each Skill has its own baseline, implementation, forward test, and structural validation gate.
- Installation and packaging exclude governance material from the runtime Skill directory.
- Publication uses an isolated agent branch and explicit file staging.
