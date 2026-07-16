# Detailed Bilingual README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the minimal English root README with a detailed Chinese team handbook and add a fact-aligned English companion.

**Architecture:** `README.md` becomes the default Chinese entry point for users and maintainers; `README_EN.md` mirrors the same core facts in tighter English. Both documents link to the existing runtime Skills, governance records, and `INSTALL.md` instead of duplicating internal rule files.

**Tech Stack:** Markdown, PowerShell, Git, repository-relative links.

## Global Constraints

- Do not change any runtime Skill trigger, behavior, or governance policy.
- Keep `INSTALL.md` as the detailed installation guide.
- Keep `governance/` outside runtime installation context.
- The central suite remains proposal-only by default.
- A personal branch requires explicit opt-in and a distinct Skill name.
- Do not bind examples to a specific ERP, marketplace, accounting tool, threshold, or financial definition.
- Use repository-relative links only; do not include machine-specific paths.
- Chinese is the default README language; English lives in `README_EN.md`.
- Deliver the same README revision to the local repository, the local team-sharing ZIP, and the GitHub default branch.

---

### Task 1: Build the Chinese Team Handbook

**Files:**
- Modify: `README.md`
- Reference: `docs/design/2026-07-16-detailed-bilingual-readme-design.md`
- Reference: `runtime/orchestrating-skill-work/references/routing-rules.md`
- Reference: `runtime/governing-skill-evolution/references/branch-policy.md`
- Reference: `runtime/governing-skill-evolution/references/improvement-protocol.md`
- Reference: `INSTALL.md`

**Interfaces:**
- Consumes: The five runtime Skill names and the approved governance policies already stored in the repository.
- Produces: A Chinese root README with stable headings and links that Task 2 mirrors.

- [ ] **Step 1: Run the pre-change Chinese coverage check**

Run:

```powershell
$text = Get-Content -Raw -Encoding UTF8 README.md
$required = @('中文', '审批式迭代', '跨境电商', '个人分支', 'README_EN.md')
$missing = $required | Where-Object { $text -notmatch [regex]::Escape($_) }
if ($missing.Count -eq 0) { throw 'Expected the current README to lack detailed Chinese coverage.' }
$missing
```

Expected: the command prints all or most required terms, proving the current README is incomplete.

- [ ] **Step 2: Replace `README.md` with the Chinese document contract**

The file must use this exact top-level order:

```markdown
# Skill 拆解、优化与治理套件

[简体中文](README.md) | [English](README_EN.md)

> 一套用于拆解、优化、评测、编排和持续治理 AI Skill 的五 Skill 协作体系。

## 这套工具解决什么问题
## 适用与不适用场景
## 五个 Skill 如何分工
## 如何选择正确的 Skill
## 完整工作流程
## 审批式迭代机制
## 中央版本与个人分支
## 跨境电商团队应用示例
## 仓库结构
## 快速安装
## 第一次使用
## 常用提示词
## 标准输出物与证据要求
## 评测、发布与回滚
## 常见问题
## 贡献和维护
## 版本状态
```

Within those sections, include all of the following exact operational facts:

```markdown
- `analyzing-skills` performs read-only decomposition and never treats findings as edit authorization.
- `improving-skills` handles approved modification, restructuring, splitting, or derived versions.
- `evaluating-skills` tests triggers, normal behavior, failure paths, regression, and release readiness.
- `governing-skill-evolution` manages proposals, approvals, versions, branches, merge, release, and rollback.
- `orchestrating-skill-work` is the entry point when one request spans two or more stages.
- The central suite accepts improvement proposals by default.
- A personal branch exists only after the user explicitly selects it, uses a distinct Skill name, and does not automatically overwrite the central suite.
- Runtime installation copies only the five child directories under `runtime/`; `governance/` remains maintenance and test material.
```

Include three e-commerce scenarios as four-column tables with `场景`, `推荐流程`, `关键输入`, and `主要产物`:

```markdown
| ERP 销售、库存和广告表格流程 | 拆解 → 改进提案 → 获批实现 → 评测 | 原 Skill、字段说明、样例表、业务口径 | 分析简报、派生 Skill、测试报告 |
| 平台对账单到标准财务账单 | 拆解 → 风险审查 → 获批实现 → 评测 | 对账单、字段映射、币种与期间、输出模板 | 财务处理 Skill、异常规则、标准账单 |
| 外部 Skill 的公司化适配 | 只读拆解 → 差异表 → 改进提案 | 完整 Skill 包、依赖文件、公司规则 | 证据表、缺口清单、变更计划 |
```

Each scenario must state that example fields and thresholds are illustrative and that the user supplies the authoritative business definition.

- [ ] **Step 3: Run the Chinese content check**

Run:

```powershell
$text = Get-Content -Raw -Encoding UTF8 README.md
$required = @(
  '# Skill 拆解、优化与治理套件',
  '[English](README_EN.md)',
  'analyzing-skills',
  'improving-skills',
  'evaluating-skills',
  'governing-skill-evolution',
  'orchestrating-skill-work',
  '审批式迭代机制',
  '中央版本与个人分支',
  '跨境电商团队应用示例',
  'governance/'
)
$missing = $required | Where-Object { -not $text.Contains($_) }
if ($missing.Count -gt 0) { throw ('Missing Chinese README content: ' + ($missing -join ', ')) }
'Chinese README content check passed.'
```

Expected: `Chinese README content check passed.`

- [ ] **Step 4: Commit the Chinese handbook**

```powershell
git add README.md
git commit -m "docs: add detailed Chinese handbook"
```

Expected: one commit containing only `README.md`.

---

### Task 2: Add the English Companion

**Files:**
- Create: `README_EN.md`
- Reference: `README.md`

**Interfaces:**
- Consumes: The headings, facts, Skill names, governance model, and relative links established in Task 1.
- Produces: An English document that is independently usable and links back to the Chinese source.

- [ ] **Step 1: Run the pre-change English file check**

Run:

```powershell
if (Test-Path README_EN.md) { throw 'README_EN.md already exists; inspect it before replacing.' }
'README_EN.md is absent as expected.'
```

Expected: `README_EN.md is absent as expected.`

- [ ] **Step 2: Create `README_EN.md` with aligned headings**

Use this exact top-level order:

```markdown
# Skill Analysis, Improvement, and Governance Suite

[简体中文](README.md) | [English](README_EN.md)

> A coordinated five-Skill suite for analyzing, improving, evaluating, orchestrating, and governing AI Skills.

## What This Suite Solves
## When to Use It
## The Five Runtime Skills
## Routing a Request
## End-to-End Workflow
## Approval-Gated Evolution
## Central Version and Personal Branches
## Cross-Border E-Commerce Examples
## Repository Layout
## Quick Installation
## First Use
## Prompt Examples
## Artifacts and Evidence
## Evaluation, Release, and Rollback
## Troubleshooting
## Contributing and Maintenance
## Release Status
```

The English document must preserve the same five Skill responsibilities and these governance statements:

```markdown
- Analysis is read-only and does not grant permission to edit source material.
- Central changes are proposal-only by default.
- Implementation follows explicit approval of the exact proposal and target.
- Personal branches require explicit opt-in, distinct naming, provenance, compatibility notes, and their own test evidence.
- Governance records are not installed as runtime Skill context.
```

Provide English versions of the same three e-commerce cases without adding new business rules.

- [ ] **Step 3: Run the English alignment check**

Run:

```powershell
$zh = Get-Content -Raw -Encoding UTF8 README.md
$en = Get-Content -Raw -Encoding UTF8 README_EN.md
$skills = @('analyzing-skills','improving-skills','evaluating-skills','governing-skill-evolution','orchestrating-skill-work')
$missingZh = $skills | Where-Object { -not $zh.Contains($_) }
$missingEn = $skills | Where-Object { -not $en.Contains($_) }
if ($missingZh.Count -gt 0 -or $missingEn.Count -gt 0) { throw 'A Skill name is missing from one language.' }
if (-not $en.Contains('[简体中文](README.md)')) { throw 'English-to-Chinese language link is missing.' }
'Bilingual Skill-name and language-link check passed.'
```

Expected: `Bilingual Skill-name and language-link check passed.`

- [ ] **Step 4: Commit the English companion**

```powershell
git add README_EN.md
git commit -m "docs: add English README companion"
```

Expected: one commit containing only `README_EN.md`.

---

### Task 3: Validate Links, Refresh Local Deliverables, and Publish

**Files:**
- Verify: `README.md`
- Verify: `README_EN.md`
- Verify: `INSTALL.md`
- Verify: `runtime/*/SKILL.md`
- Verify: `runtime/governing-skill-evolution/references/branch-policy.md`
- Verify: `runtime/governing-skill-evolution/references/improvement-protocol.md`
- Verify: `governance/release/manifest.md`

**Interfaces:**
- Consumes: Both completed README files and all existing repository targets they reference.
- Produces: Verification evidence, updated local files, a refreshed team-sharing ZIP, a clean documentation-only diff, and the same revision on GitHub.

- [ ] **Step 1: Verify every relative Markdown link**

Run:

```powershell
$errors = @()
foreach ($file in @('README.md','README_EN.md')) {
  $text = Get-Content -Raw -Encoding UTF8 $file
  $matches = [regex]::Matches($text, '\[[^\]]+\]\(([^)#]+)(?:#[^)]+)?\)')
  foreach ($match in $matches) {
    $target = $match.Groups[1].Value
    if ($target -notmatch '^(https?://|mailto:)' -and -not (Test-Path -LiteralPath $target)) {
      $errors += "$file -> $target"
    }
  }
}
if ($errors.Count -gt 0) { throw ('Broken links: ' + ($errors -join '; ')) }
'Relative-link check passed.'
```

Expected: `Relative-link check passed.`

- [ ] **Step 2: Verify the runtime inventory and forbidden installation claim**

Run:

```powershell
$expected = @('analyzing-skills','evaluating-skills','governing-skill-evolution','improving-skills','orchestrating-skill-work') | Sort-Object
$actual = Get-ChildItem runtime -Directory | Select-Object -ExpandProperty Name | Sort-Object
if (Compare-Object $expected $actual) { throw 'Runtime Skill inventory differs from the README contract.' }
$docs = (Get-Content -Raw -Encoding UTF8 README.md) + (Get-Content -Raw -Encoding UTF8 README_EN.md)
if (-not $docs.Contains('governance/')) { throw 'The governance runtime boundary is not documented.' }
'Runtime inventory check passed.'
```

Expected: `Runtime inventory check passed.`

- [ ] **Step 3: Scan for unfinished content and machine-specific paths**

Run:

```powershell
$files = @('README.md','README_EN.md')
$patterns = @('TO[D]O','TB[D]','C:\\Users\\','/Users/','<your-','填写')
$hits = foreach ($file in $files) {
  foreach ($pattern in $patterns) {
    Select-String -Path $file -Pattern $pattern
  }
}
if ($hits) { $hits | Format-Table; throw 'Unfinished or machine-specific content found.' }
'Content hygiene check passed.'
```

Expected: `Content hygiene check passed.`

- [ ] **Step 4: Rebuild and verify the local team-sharing ZIP**

Run from the repository root:

```powershell
$zip = '..\outputs\analyzing-and-improving-skills-1.0.0.zip'
Compress-Archive -Path @('runtime','governance','docs','README.md','README_EN.md','INSTALL.md') -DestinationPath $zip -Force
$archive = [System.IO.Compression.ZipFile]::OpenRead((Resolve-Path $zip))
try {
  $names = $archive.Entries.FullName
  foreach ($required in @('README.md','README_EN.md','INSTALL.md')) {
    if ($names -notcontains $required) { throw "$required is missing from the team-sharing ZIP." }
  }
  if ($names -match '(^|/)\.git(/|$)') { throw 'The team-sharing ZIP contains Git metadata.' }
} finally {
  $archive.Dispose()
}
Get-FileHash -Algorithm SHA256 $zip
```

Expected: the ZIP contains both README files and `INSTALL.md`, contains no `.git` entry, and prints a SHA-256 hash.

- [ ] **Step 5: Review the complete documentation diff**

Run:

```powershell
git status -sb
git diff origin/main...HEAD --stat
git diff origin/main...HEAD -- README.md README_EN.md docs/design/2026-07-16-detailed-bilingual-readme-design.md docs/superpowers/plans/2026-07-16-detailed-bilingual-readme.md
```

Expected: only the design document, implementation plan, `README.md`, and `README_EN.md` differ from `origin/main`; no runtime or governance rule file is modified.

- [ ] **Step 6: Commit the implementation plan if it is not already committed**

```powershell
git add docs/superpowers/plans/2026-07-16-detailed-bilingual-readme.md
git commit -m "docs: plan detailed bilingual README"
```

Expected: the plan is recorded in branch history before publication.

- [ ] **Step 7: Push, review, and merge the GitHub change**

Run:

```powershell
git push -u origin agent/detailed-bilingual-readme
```

Then open a PR targeting `main` with:

```text
Title: Add detailed Chinese and English README guides

Summary:
- make Chinese the default project README
- add a linked English companion
- document routing, approvals, personal branches, e-commerce examples, testing, and maintenance

Validation:
- bilingual content checks passed
- relative-link check passed
- runtime inventory check passed
- content hygiene check passed
```

After checks succeed, merge the PR using a squash merge. Verify all of the following against GitHub after merge:

```text
- PR state is MERGED
- README.md exists on main
- README_EN.md exists on main
- main points to the merge commit
```

Expected: the local repository, local ZIP, and GitHub `main` all contain the same detailed bilingual README revision.
