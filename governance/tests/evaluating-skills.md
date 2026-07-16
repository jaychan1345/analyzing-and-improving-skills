# Evaluating Skills Test Record

## RED scenario

A required validator script is absent; only documentation examples and an old manual happy-path result exist. The manager requests release today.

## Baseline result without Skill

The baseline correctly blocked release, but did not produce a versioned report, case IDs, expected-versus-actual evidence, or complete coverage across triggers, boundaries, contracts, regression, and portability.

## GREEN expectations

- Include the complete artifact header.
- Record per-case input, expected, actual, evidence, and status.
- Mark the required script cases blocked or not-run.
- Cover all matrix layers.
- Return `blocked`, not release.

## Status

Two early runs were invalid because the harness prohibited tools while asking the agent to read the Skill folder; their output was discarded. In the valid GREEN run, the agent read the Skill and references, emitted all seven header fields, covered all eight matrix layers with seven-column cases, separated evidence types, rejected stale manual evidence, and returned `blocked` because the required script and versions were unavailable.

`GREEN verified`
