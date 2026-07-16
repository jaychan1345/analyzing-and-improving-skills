---
name: improving-skills
description: Use when a user explicitly asks to modify, optimize, split, restructure, or create a derived version of an existing Skill; 当用户明确要求优化、修改、拆分、重构或生成已有 Skill 的衍生版本时使用。
---

# Improving Skills

## Overview

把 `analysis-brief` 和新增需求转换为可审批的 `change-plan`，批准后生成非破坏性衍生 Skill。核心原则：先批准差异，再派生；永不覆盖来源。

开始前完整读取：

- `references/change-classification.md`
- `references/architecture-decisions.md`
- `references/change-plan-template.md`

## Workflow

1. 读取 `analysis-brief`、来源版本和新增需求。没有证据化分析时，先调用 `analyzing-skills`。
2. 把每项内容分类为保留、修改、新增、删除或拆分，并关联需求来源和证据。
3. 选择目标架构、新 `name`、受影响文件、迁移方式和回滚方式。
4. 定义新增触发、功能、异常、边界和回归用例。
5. 输出完整 `change-plan`，状态设为 `awaiting-change-approval`，然后停止。
   完成前核对全部头字段；未知值写 `unknown`，不使用 `TBD` 或删除字段。
6. 仅在用户明确批准该 `case_id`、产物版本和目标名称后生成衍生 Skill。
7. 保留来源文件不变；用户要求覆盖时，改为新名称、新版本或明确选择的个人分支。
8. 生成后交给 `evaluating-skills`；本 Skill 不作发布结论。

## Decision Rules

- description 只写触发条件和相邻边界，不写完整输入、输出或流程捷径。
- 只有重复、确定、易错的操作需要脚本；否则使用清晰文字规则。
- 业务审批规则与 `change-plan` 审批分开定义。
- 冲突需求列出方案、影响和待选项，不自行选核心业务口径。

## Quick Reference

| Situation | Required action |
|---|---|
| 用户说“直接改” | 仍先输出 `change-plan` |
| 用户要求覆盖原件 | 改为衍生名称/版本/个人分支 |
| 核心口径冲突 | `blocked-by-business-rule` |
| 只改一句 description | 仍需触发回归用例 |
| 新增脚本 | 定义接口、失败行为和执行测试 |

## Common Mistakes

- 把备份后覆盖当作非破坏性优化。
- 把过去的一般同意当作当前计划批准。
- 未经批准就创建衍生文件。
- 为了“更完整”提前添加无证据需要的脚本或资产。
- 生成新版后自行声称可发布。
