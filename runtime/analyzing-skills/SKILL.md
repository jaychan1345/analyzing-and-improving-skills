---
name: analyzing-skills
description: Use when a user asks to inspect, explain, audit, reverse engineer, or decompose one SKILL.md or a complete Skill package without changing it; 当用户只要求检查、解释、审计、逆向分析或拆解 Skill 且不要求修改时使用。
---

# Analyzing Skills

## Overview

对 Skill 做只读、证据化拆解，输出范围明确的 `analysis-brief`。核心原则：缺失内容保持缺失；事实、推断、问题和建议分开。

开始前完整读取：

- `references/analysis-framework.md`
- `references/evidence-rules.md`
- `references/analysis-brief-template.md`

## Workflow

1. 确认分析范围：单个 `SKILL.md` 或完整目录。单文件不得宣称完成包级分析。
2. 盘点实际提供的文件与可访问内容，建立文件树和引用表。
3. 对每个引用标记 `present`、`missing`、`external` 或 `unverified`。
4. 按分析框架提取目标、边界、触发、输入、状态、规则、知识、工具、输出、异常和验收。
5. 给每条结论标记证据等级并引用来源位置。
6. 使用固定模板生成版本化 `analysis-brief`。不修改来源文件。
7. 完成前核对模板的全部头字段和章节；未知值写 `unknown`，不要省略字段。

## Evidence Rules

- `FACT`：来源中直接存在，可引用文件与段落。
- `INFERENCE`：由事实推导，必须写明依据与不确定性。
- `MISSING`：被引用但未提供；不得补写其内容。
- `ISSUE`：事实与合同之间的缺口或冲突。
- `OPPORTUNITY`：改进候选，不是来源当前行为。

用户允许“合理假设”时，只能增加 `INFERENCE`，不能把它升级为 `FACT` 或精确合同。

## Quick Reference

| Input | Allowed conclusion |
|---|---|
| 单个文件 | 文件级行为与缺失依赖 |
| 完整包 | 文件树、引用完整性和跨文件合同 |
| 缺失 reference/script/asset | 仅记录依赖名称、用途线索和不可验证影响 |
| 无法运行脚本 | 记录静态观察；运行行为 `unverified` |

## Example

若正文写“读取 `references/fields.md`”，但文件未提供：事实是“存在该引用”；缺失项是“字段定义不可访问”；不能输出 SKU、库存数量等“默认字段”。

## Common Mistakes

- 用行业常识补齐缺失 reference。
- 把建议报告结构写成来源输出合同。
- 不区分单文件分析和完整包分析。
- 只总结标题，不重建状态、失败和验收。
- 发现问题后直接修改来源 Skill。
