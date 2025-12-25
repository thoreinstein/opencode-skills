---
name: postmortem
description: Generate blameless postmortem with root cause analysis
---

# Post-Incident Review

**Current Time:** !`date`

Generate a blameless postmortem document with root cause analysis. Investigates the incident and codebase to provide deeper RCA insights.

## Input

- Incident reference (Obsidian incident file path or summary)
- Resolution details (what fixed it, when)
- Optional: additional context, timeline notes

## Investigation Strategy

Launch three parallel investigation tracks to deepen RCA:

### Track 1: External Research (librarian agent)

- Research similar incidents in public postmortems
- Find industry best practices for preventing recurrence
- Identify patterns from similar failures

### Track 2: Codebase Exploration (explore agent)

- Trace the full failure path through the codebase
- Identify systemic issues (missing tests, error handling gaps)
- Find related code that may have similar vulnerabilities
- Review monitoring/alerting coverage for affected paths

### Track 3: Code Analysis (inferred agent: go/frontend/postgres/etc.)

- Infer appropriate agent from incident context
- Deep analysis of root cause code
- Identify contributing technical factors
- Assess fix completeness and durability

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Postmortems/YYYY-MM-DD-incident-title.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/postmortem.md

## Behavior

1. Parse incident reference to extract context (read from Obsidian if path provided)
2. Infer appropriate code agent from incident context
3. Launch librarian, explore, and inferred code agent in parallel
4. Analyze failure path and identify systemic issues
5. Generate 5 Whys analysis based on findings
6. Synthesize into blameless postmortem document
7. Write to Obsidian via `obsidian_append_content` with auto-generated filename: `YYYY-MM-DD-incident-title.md`
8. Include wiki-link back to original incident document

$ARGUMENTS
