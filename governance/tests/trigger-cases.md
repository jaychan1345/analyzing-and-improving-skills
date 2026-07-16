# Trigger Cases

| ID | Request | Expected first Skill |
|---|---|---|
| TR-01 | “拆解这个 SKILL.md，说明触发、输入、流程和缺失依赖。” | `analyzing-skills` |
| TR-02 | “基于拆解结果增加审批并生成 V2，但保留原 Skill。” | `improving-skills` |
| TR-03 | “测试这个 Skill 会不会误触发，并判断能否发布。” | `evaluating-skills` |
| TR-04 | “把这次流程问题提交为中心版本改进提案。” | `governing-skill-evolution` |
| TR-05 | “拆解、优化、测试并准备安装这个 Skill。” | `orchestrating-skill-work` |

## Adjacent negative cases

| ID | Request | Must not be routed first to |
|---|---|---|
| TN-01 | “只解释 SKILL.md，不要修改。” | `improving-skills` |
| TN-02 | “只测试现有 Skill，不生成新版。” | `improving-skills` |
| TN-03 | “优化目标 Skill，不修改拆解体系本身。” | `governing-skill-evolution` |
| TN-04 | “单独分析一个 Skill。” | `orchestrating-skill-work` |
