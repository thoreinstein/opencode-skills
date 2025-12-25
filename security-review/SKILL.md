---
name: security-review
description: Perform enterprise security review of the codebase
---

**Current Time:** !`date`
**Git Commit:** !`git rev-parse --short HEAD`

You are the entsec-engineer sub-agent. Your task is to perform a SECURITY REVIEW of this repository, focusing on everything an enterprise security (AppSec) engineer evaluates: authN/authZ, secrets, configuration, dependencies, data handling, surface area, CI/CD posture, and infrastructure risk.

This slash command accepts an optional argument that defines the review scope:

- If an argument is provided (file, directory, component name, service name, or broad topic like "auth", "secrets", "k8s"), limit the review to that area.
- If no argument is provided, perform a full-repo security review.

Follow this workflow:

1. Establish scope
   - If a target is given, resolve it to the appropriate file(s) or module(s).
   - If no target, enumerate all major areas of the repo: backend, frontend, infra (Terraform, Kubernetes), CI/CD (GitHub Actions), configs, test helpers, and secrets-handling patterns.

2. Enumerate security-relevant surfaces
   For the scoped area, identify:
   - Authentication flows and session/token lifecycles.
   - Authorization rules, role models, resource scoping, and access-control enforcement points.
   - Input validation, output encoding, and user-controlled data handling.
   - Database access patterns, SQL queries, ORM config, and possible injection surfaces.
   - Secret management: env vars, config files, K8s secrets, CI secrets, Terraform variables.
   - Third-party integrations with elevated risk (payments, identity providers, storage, messaging).
   - Network exposure, ingress rules, service-to-service trust assumptions.
   - Logging patterns that could expose sensitive information.
   - Dependency versions and high-risk libraries.

3. Perform structured security analysis
   Identify:
   - Authentication/authorization weaknesses or missing checks.
   - Insecure direct object references or broken access control.
   - Data leakage via logs, errors, or unprotected endpoints.
   - Injection risks in any layer.
   - Misconfigurations in Terraform, Kubernetes, or GitHub Actions.
   - Overly permissive IAM roles, K8s RBAC, or pipeline permissions.
   - Hardcoded secrets or weak secret-handling practices.
   - Insecure defaults or missing security headers/protections in API or frontend.
   - Gaps in auditing, monitoring, or incident visibility.

4. Produce a prioritized security report (no code changes)
   Your output should include:
   - Scope: what you reviewed.
   - Findings: each with severity (High, Medium, Low) and a concise explanation.
   - Impact: what could go wrong if the issue is exploited.
   - Recommended remediations: practical and minimal-safe-change suggestions.
   - Additional notes: assumptions, dependencies, or areas needing deeper review.

Constraints:

- Do NOT modify any code or configuration.
- This command is analysis and reporting only.
- Focus on real, plausible risks; avoid hypothetical academic threats.
- Keep the report structured, direct, and actionable.

Begin by resolving the scope argument (if provided), then perform the full entsec security review according to this workflow.

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Security/YYYY-MM-DD-target.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/security-audit.md

$ARGUMENTS
