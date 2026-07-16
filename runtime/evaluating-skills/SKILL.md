---
name: evaluating-skills
description: Use when a user asks to test, validate, review, compare, or decide whether a Skill or derived version is ready to release; 当用户要求测试、验证、评审、比较或判断 Skill 是否具备发布条件时使用。
---

# Evaluating Skills

## Overview

用可复现证据评测 Skill，并输出 `evaluation-report`。核心原则：静态审阅、运行验证和未验证项分别记录；测试失败不能靠改业务规则绕过。

开始前完整读取：

- `references/test-matrix.md`
- `references/evaluation-rubric.md`
- `references/evaluation-report-template.md`

## Workflow

1. 记录环境、来源版本、目标版本、可用依赖和限制。
2. 从触发描述、输入合同、业务规则、输出合同和验收标准生成用例。
3. 覆盖触发、边界、正常、缺失、异常、输出、重复执行、回归和可移植性。
4. 对每个用例记录 ID、类型、输入、预期、实际、证据和状态。
5. 区分 `passed`、`failed`、`blocked` 和 `not-run`；文档看起来正确不等于运行通过。
6. 按评分规则输出 `release`、`revise` 或 `blocked`。任何关键失败、缺失必需依赖或未运行关键用例都不能 `release`。
7. 返回修正阶段时指出失败归因：来源不完整回分析，规则或实现缺陷回优化。

## Required Output Shape

最终输出就是 `references/evaluation-report-template.md` 的结构，顺序固定：七字段 YAML 头 → 环境与版本 → 限制与未验证项 → 七列用例表 → 八层覆盖摘要 → 关键失败 → 非关键发现 → 单一 verdict。

用例表必须分别出现 `trigger`、`function`、`missing`、`abnormal`、`contract`、`repeatability`、`regression`、`portability` 八种类型。若无法执行，仍保留该行并把 `Actual` 写成无法执行的原因，`Status` 写 `blocked` 或 `not-run`。

完成前逐项核对：七个头字段、八种用例类型、七个用例列和一个合法 verdict 均存在。

## Evidence Rules

- `static`：来自文件内容或结构。
- `executed`：来自实际命令、输出、退出码或产物。
- `observed`：来自真实交互或触发结果。
- `unverified`：缺少环境、依赖、权限或黄金样例。

不得把上月的手工结果当作当前版本回归证据。

## Quick Reference

| Condition | Verdict impact |
|---|---|
| 必需脚本缺失 | `blocked` |
| 关键用例 `not-run` | 不得发布 |
| description 误触发 | `revise` |
| 输出无法定义正确性 | `blocked`，等待黄金样例 |
| 非关键文案问题 | 可 `revise`，不冒充功能失败 |

## Common Mistakes

- 只测一个 happy path。
- 用代码审阅替代实际执行。
- 为让测试通过而修改期望业务规则。
- 只写结论，不保留预期、实际和证据。
- 把旧版本测试结果套到新版本。
