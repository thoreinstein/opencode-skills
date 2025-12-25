---
name: deploy
description: Generate deployment checklist with pre-flight checks and rollout strategy
---

# Deployment Checklist & Pre-flight

**Current Time:** !`date`
**K8s Context:** !`kubectl config current-context`

Generate a deployment checklist with pre-flight checks, rollout strategy, and verification steps. Documents to Obsidian.

## Input

- Target: service, environment, or release
- Scope: what's being deployed (commits, features, fixes)
- Optional: deployment strategy preference (rolling, blue-green, canary)

## Investigation Strategy

Launch parallel investigation tracks:

### Track 1: Codebase Exploration (explore agent)

- Identify changes included in deployment
- Find database migrations
- Detect configuration changes
- Map affected services and dependencies
- Locate feature flags

### Track 2: Infrastructure Analysis (inferred agent: k8s/gcp-dev)

- Review deployment manifests
- Check resource requirements
- Verify environment configuration
- Assess scaling and rollout settings

### Track 3: External Research (librarian agent)

- Check for known issues with dependencies being updated
- Find deployment best practices for change types

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Deployments/YYYY-MM-DD-HHMM-service-env.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/deploy-checklist.md

## Behavior

1. Parse target to identify service, environment, and scope
2. Infer appropriate infrastructure agent (k8s, gcp-dev)
3. Launch explore, librarian, and inferred agent in parallel
4. Identify all changes, migrations, and config updates
5. Generate appropriate rollout strategy
6. Create pre-flight and verification checklists
7. Write deployment doc to Obsidian via `obsidian_append_content` with auto-generated filename: `YYYY-MM-DD-HHMM-service-env.md`

$ARGUMENTS
