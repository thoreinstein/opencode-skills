---
name: deps
description: Analyze dependencies for security vulnerabilities, outdated packages, and license compliance
---

# Dependency Analysis & Management

**Current Time:** !`date`
**Go Version:** !`go version`

Analyze project dependencies for security vulnerabilities, outdated packages, and license compliance. Documents findings to Obsidian.

## Input

- Scope: full audit, security-only, updates-only, or licenses-only
- Optional: specific package to investigate
- Optional: target version constraints

## Investigation Strategy

Launch parallel investigation tracks:

### Track 1: Security Analysis

- Run `govulncheck` for Go vulnerabilities
- Run `npm audit` for JavaScript vulnerabilities
- Cross-reference with CVE databases
- Assess severity and exploitability

### Track 2: Update Analysis

- Check for outdated direct dependencies
- Identify major version updates (breaking changes)
- Review changelogs for significant updates
- Assess update risk and effort

### Track 3: External Research (librarian agent)

- Research CVE details and exploit availability
- Find migration guides for major updates
- Check for known issues with newer versions
- Identify deprecated packages needing replacement

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Dependencies/YYYY-MM-DD-audit.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/deps-audit.md

## Behavior

1. Detect project type(s) from manifest files (go.mod, package.json)
2. Run security scanners (govulncheck, npm audit)
3. Analyze outdated dependencies and categorize by risk
4. Check license compliance for all dependencies
5. Launch librarian agent for CVE research on critical/high findings
6. Generate prioritized action items
7. Write audit report to Obsidian via `obsidian_append_content` with auto-generated filename: `YYYY-MM-DD-audit.md`

## Commands Reference

### Go

```bash
# Vulnerability check
govulncheck ./...

# List outdated (requires go-mod-outdated)
go list -u -m all | go-mod-outdated

# Tidy dependencies
go mod tidy

# Verify checksums
go mod verify
```

### JavaScript

```bash
# Security audit
npm audit
npm audit --json

# Outdated packages
npm outdated

# License check (requires license-checker)
npx license-checker --summary
```

$ARGUMENTS
