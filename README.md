# Analyzing and Improving Skills

A reusable five-Skill suite for dissecting, improving, evaluating, orchestrating, and governing AI Skills.

## Runtime Skills

| Skill | Use it for |
|---|---|
| `analyzing-skills` | Read-only decomposition, audit, or reverse analysis |
| `improving-skills` | Approval-gated derivation or restructuring |
| `evaluating-skills` | Trigger, behavior, failure, regression, and release evaluation |
| `governing-skill-evolution` | Proposals, central versions, personal branches, merge, and rollback |
| `orchestrating-skill-work` | Requests spanning two or more stages |

`runtime/` contains installable Skills. `governance/` contains tests, fixtures, and release records and should not be installed as runtime context.

The central suite accepts improvement proposals by default. A user may maintain a personal branch only after explicitly choosing that path.

See [INSTALL.md](INSTALL.md) for installation.
