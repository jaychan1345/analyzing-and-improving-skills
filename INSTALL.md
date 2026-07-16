# Installation

## Personal installation

Copy each direct child directory of `runtime/` into the personal Codex Skill directory:

```text
~/.codex/skills/
```

The resulting layout must contain five sibling Skill directories, each with its own `SKILL.md` and `agents/openai.yaml`.

Do not copy `governance/` into the runtime Skill directory. It is maintenance and test material, not everyday agent context.

Restart Codex if newly installed Skills are not discovered immediately.

## Team sharing

Share the complete repository or a ZIP containing `runtime/`, `governance/`, `README.md`, and `INSTALL.md`. Remove local test outputs, business data, account identifiers, secrets, and machine-specific paths before distribution.

## Update policy

- Submit a proposal for changes to the central suite.
- Do not edit the central version from a single ordinary case.
- Create a personal branch only when the user explicitly selects it.
- Give a personal branch a distinct Skill name and record its source version and owner.
