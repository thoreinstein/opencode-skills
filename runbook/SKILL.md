---
name: runbook
description: Generate operational runbooks for services, procedures, or incident response
---

# Operational Runbook Generator

**Current Time:** !`date`
**K8s Context:** !`kubectl config current-context`

Generate operational runbooks for services, procedures, or incident response. Investigates the codebase and infrastructure to produce accurate, actionable procedures. Documents to Obsidian.

## Input

- Topic: service name, operation type, or incident scenario
- Scope: deployment, scaling, failover, maintenance, troubleshooting
- Optional: specific scenarios to cover

## Investigation Strategy

Launch parallel investigation tracks:

### Track 1: Codebase Exploration (explore agent)

- Identify service entry points and configuration
- Find health check endpoints
- Map dependencies (databases, caches, external services)
- Locate logging and metrics instrumentation
- Find existing scripts or automation

### Track 2: Infrastructure Analysis (inferred agent: k8s/sre/gcp-dev)

- Review deployment manifests
- Identify scaling configuration
- Map service dependencies
- Find monitoring and alerting setup
- Review backup and recovery procedures

### Track 3: External Research (librarian agent)

- Find operational best practices for the service type
- Research common failure modes
- Identify industry-standard procedures

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Runbooks/YYYY-MM-DD-service-operation.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/runbook.md

## Behavior

1. Parse topic to identify service and operation scope
2. Infer appropriate infrastructure agent (k8s, sre, gcp-dev)
3. Launch explore, librarian, and inferred agent in parallel
4. Extract configuration, endpoints, and dependencies from codebase
5. Identify common operations and failure modes
6. Generate step-by-step procedures with actual commands
7. Write runbook to Obsidian via `obsidian_append_content` with auto-generated filename: `YYYY-MM-DD-service-operation.md`

$ARGUMENTS
