---
name: rollback
description: Analyze deployment or change for rollback safety and generate checklist
---

# Rollback Analysis & Checklist

**Current Time:** !`date`
**K8s Context:** !`kubectl config current-context`

Analyze a deployment or change for rollback safety and generate a prioritized rollback checklist. Documents findings to Obsidian.

## Input

- Target: deployment, commit SHA, release tag, or PR reference
- Context: what went wrong or why rollback is being considered
- Optional: urgency level (immediate vs planned)

## Investigation Strategy

Launch parallel investigation tracks:

### Track 1: Codebase Exploration (explore agent)

- Identify all changes included in the rollback scope
- Map database migrations in the change set
- Find feature flags introduced or modified
- Identify API contract changes
- Assess backward compatibility

### Track 2: Code Analysis (inferred agent: go/frontend/postgres)

- Analyze migration reversibility
- Check for data transformations that may not be reversible
- Identify breaking changes in APIs or contracts
- Review feature flag dependencies

### Track 3: External Research (librarian agent)

- Find rollback patterns for similar changes
- Check for known rollback issues with dependencies
- Research safe rollback strategies for the change type

## Rollback Safety Assessment

### Safe to Rollback

- Code-only changes (no DB migrations)
- Additive API changes
- Feature-flagged functionality
- UI/frontend changes

### Requires Caution

- Database migrations (check reversibility)
- API breaking changes (check client compatibility)
- Configuration changes (check dependent services)
- Infrastructure changes (check state)

### Potentially Dangerous

- Destructive migrations (DROP, DELETE, column removal)
- Data transformations (may lose data)
- Schema changes with live traffic
- Multi-service coordinated deployments

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Rollbacks/YYYY-MM-DD-HHMM-target.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/rollback-analysis.md

## Behavior

1. Parse target to identify rollback scope (commits, migrations, config)
2. Infer appropriate code agent from change types
3. Launch explore, librarian, and inferred code agent in parallel
4. Assess migration reversibility and data safety
5. Identify feature flags and configuration changes
6. Generate risk assessment with specific blockers
7. Create prioritized rollback checklist with actual commands
8. Write analysis to Obsidian via `obsidian_append_content` with auto-generated filename: `YYYY-MM-DD-HHMM-target.md`

$ARGUMENTS
