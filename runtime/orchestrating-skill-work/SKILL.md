---
name: orchestrating-skill-work
description: Use when one request spans two or more stages among Skill analysis, improvement, evaluation, release, installation, or governance; 当单次请求同时涉及拆解、优化、评测、发布、安装或治理中的两个以上阶段时使用。
---

# Orchestrating Skill Work

## Overview

编排跨阶段 Skill 工作，维护状态、审批和标准产物传递。核心原则：总控只路由与汇总，不替代专业 Skill 完成拆解、修改或评测。

开始前完整读取：

- `references/routing-rules.md`
- `references/artifact-contracts.md`

## Workflow

1. 识别请求包含的阶段。只有一个阶段时直接交给对应专业 Skill；两个以上阶段时继续编排。
2. 盘点来源位置、允许的操作、期望交付、审批人和已知限制。
3. 先生成版本化 `task-brief`。没有 `task-brief`，不启动专业阶段。
   `allowed mutations` 只能是 `read-only`、`derive-new` 或已评测版本的安装；本套件不接受覆盖来源 Skill。用户要求覆盖时，改为新名称、新版本或明确的个人分支。
4. 按路由表调用专业 Skill，并把上一阶段的标准产物原样传入下一阶段：
   - **REQUIRED SUB-SKILL:** Use `analyzing-skills` for read-only decomposition.
   - **REQUIRED SUB-SKILL:** Use `improving-skills` for change planning and derivation.
   - **REQUIRED SUB-SKILL:** Use `evaluating-skills` for validation and release evidence.
   - **REQUIRED SUB-SKILL:** Use `governing-skill-evolution` for changes to this suite itself.
5. 在范围、变更、发布和流程改进门槛处停止，关联具体产物并取得当前审批。
   目标 Skill 内的财务、法务或业务审批属于待定义的业务规则，不自动等同于本套件的变更审批。分别记录审批角色、证据、时点、拒绝和超时处理。
6. 失败时按原因返回正确阶段；不要绕过失败或替专业 Skill 改规则。
7. 汇总最终交付、版本、限制、未验证项、安装位置和后续决定。

## State Rules

使用以下主状态：`received → source-checked → analyzed → awaiting-change-approval → derived → evaluating → awaiting-release-approval → released`。

异常使用 `incomplete`、`evaluation-failed`、`blocked-by-business-rule` 或 `blocked-by-permission`。只有证据支持时才推进状态。

## Quick Reference

| Situation | Action |
|---|---|
| 单阶段请求 | 直接路由专业 Skill |
| 跨两个以上阶段 | 创建 `task-brief` 并编排 |
| 缺失来源或依赖 | 标记 `incomplete`，不猜测 |
| `change-plan` 未批准 | 停在 `awaiting-change-approval` |
| 评测失败或未执行 | 停在 `evaluation-failed` |
| 涉及套件自身改进 | 路由治理 Skill |

## Example

请求“拆解、优化、测试并安装这个 Skill”时，先输出 `task-brief`，再依次接收 `analysis-brief`、获批的 `change-plan` 和 `evaluation-report`；总控不自行改写目标 `SKILL.md`。

## Common Mistakes

- 直接开始拆解而没有 `task-brief`。
- 在一次回复里包办分析、修改和评测。
- 把一般性同意当作当前变更或发布审批。
- 把目标业务流程中的财务审批当作 `change-plan` 的批准人。
- 自建 changelog 等非合同产物，导致下游重新猜测。
- 测试失败后仍进入安装或发布。
- 把用户对覆盖原件的同意当成有效变更模式。
