# Evidence Rules

| Label | Required support | Allowed wording |
|---|---|---|
| `FACT` | Direct source text or observed file | “The source states…” |
| `INFERENCE` | One or more cited facts plus reasoning | “This suggests…; confidence…” |
| `MISSING` | Referenced or required item not supplied | “Cannot verify…” |
| `ISSUE` | Observable conflict, omission, or mismatch | “The source requires X but provides no Y.” |
| `OPPORTUNITY` | Proposed future improvement | “A derived version could…” |

Rules:

- Cite a relative file path and heading or line when available.
- Never cite a missing file as evidence for its presumed contents.
- Keep domain familiarity outside `FACT` unless the source explicitly adopts it.
- Do not convert an example into a universal rule.
- If a script is present but unexecuted, separate static code facts from runtime claims.
- If only `SKILL.md` is supplied, label package completeness `unverified`.
