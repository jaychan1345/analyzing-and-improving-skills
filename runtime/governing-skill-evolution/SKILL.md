---
name: governing-skill-evolution
description: Use when a user asks to propose, approve, version, branch, merge, release, or roll back changes to the Skill analysis suite itself; 当用户要求管理拆解体系自身的改进提案、审批、版本、分支、合并、发布或回滚时使用。
---

# Governing Skill Evolution

## Overview

治理本套件自身的变化，区分中心版本、改进提案和个人分支。核心原则：默认只提交提案；个人分支需明确选择；中心变更需证据、回归和维护人批准。

开始前完整读取：

- `references/improvement-protocol.md`
- `references/branch-policy.md`
- `references/improvement-proposal-template.md`

## Workflow

1. 确认问题针对本套件而非某个目标 Skill；目标 Skill 优化交给 `improving-skills`。
2. 收集失败症状、案例证据、出现范围、风险和上下文成本。
3. 生成版本化 `improvement-proposal`。默认状态为 `proposed`，不自动实现。
4. 判断目标：
   - 单个普通案例 → 保持提案或局部业务配置候选。
   - 两个以上不同案例或高风险缺陷 → 可申请中心改进评审。
   - 用户明确选择个人定制 → 可规划个人分支。
5. 为任何候选改动定义旧版失败、新版通过的回归用例。
6. 中心变更只有在维护人批准并通过相关回归、端到端测试后才能发布。
7. 个人分支使用不同 `name`，记录来源、所有者、个人规则和范围；合并中心时重新走提案与评测。

## Non-Bypassable Gates

- 部门负责人、截止期或一般性赞同不能替代维护人对中心版本的批准。
- 不存在“紧急口头发布”旁路；高风险问题可以提高优先级，但仍需回归和明确批准。
- 不自动创建个人分支；必须记录用户的明确选择。
- 其他使用者的本地变更不会自动同步回中心。

## Quick Reference

| Evidence | Default result |
|---|---|
| 单个普通案例 | `improvement-proposal`，不实现 |
| 两个不同案例 | 可进入中心评审，不等于批准 |
| 高风险缺陷 | 可进入中心评审，优先处理 |
| 用户明确要个人规则 | 个人分支计划 |
| 无回归用例 | 不得合并或发布 |
| 维护人不可用 | 保持提案状态 |

## Common Mistakes

- 把公司特有字段写进所有用户的中心流程。
- 提案后自动创建 feature 或 personal branch。
- 用回滚方案代替发布前回归。
- 让部门赞助人绕过中心维护人。
- 个人分支复用中心 Skill 名称。
