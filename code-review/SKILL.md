---
name: code-review
description: Code review mode - comprehensive review with security, performance, and maintainability focus
---

# CODE REVIEW MODE

**Current Time:** !`date`
**Git Commit:** !`git rev-parse --short HEAD`

Perform a comprehensive code review using the Principal Engineer agent.

## Review Protocol

### Phase 1: Context Gathering

First, understand what changed:

```
git diff [base] -- [files]
git log --oneline -10 -- [files]
```

Launch exploration if needed:

```
background_task(agent="explore", prompt="Find related code and tests...")
```

### Phase 2: Multi-Dimensional Review

Request Principal review with full context:

```
@principal Please perform a thorough code review:

## Changes to Review
$ARGUMENTS

## Review Dimensions

### 1. Correctness
- [ ] Logic is correct for all cases
- [ ] Edge cases are handled
- [ ] Assumptions are valid
- [ ] Error states are managed

### 2. Security
- [ ] No injection vulnerabilities (SQL, XSS, command)
- [ ] Input validation is present and complete
- [ ] Sensitive data is protected
- [ ] Authentication/authorization is correct
- [ ] No secrets in code
- [ ] Dependencies are secure

### 3. Performance
- [ ] No unnecessary operations or loops
- [ ] Efficient algorithms for the scale
- [ ] No memory leaks or resource exhaustion
- [ ] Database queries are optimized (no N+1)
- [ ] Appropriate caching if needed

### 4. Reliability
- [ ] Error handling is comprehensive
- [ ] Failures are graceful
- [ ] Retry logic where appropriate
- [ ] Resource cleanup is guaranteed

### 5. Maintainability
- [ ] Code is readable and self-documenting
- [ ] Functions are focused (single responsibility)
- [ ] Naming is clear and consistent
- [ ] No unnecessary duplication
- [ ] Follows existing patterns

### 6. Testing
- [ ] Tests exist for new functionality
- [ ] Edge cases are tested
- [ ] Error paths are tested
- [ ] Tests are reliable (not flaky)
```

### Phase 3: Specialist Consultation (If Needed)

For specific concerns:

| Concern                | Agent        | Focus                                |
| ---------------------- | ------------ | ------------------------------------ |
| Security issues        | `@security`  | Deep vulnerability analysis          |
| Reliability concerns   | `@sre`       | Scalability, SLOs, observability     |
| Performance concerns   | `@perf`      | Profiling, bottlenecks, optimization |
| Architecture questions | `@architect` | Design patterns, structure           |
| Test strategy          | `@testing`   | Coverage, approach                   |

## Review Output Format

```markdown
## Summary

[APPROVE / NEEDS WORK / BLOCK] — [one-line summary]

## Critical Issues (must fix before merge)

- [ ] **[SECURITY]** [Issue] at `file:line`
  - Impact: [what could go wrong]
  - Fix: [how to fix]

## High Priority (should fix before merge)

- [ ] **[BUG]** [Issue] at `file:line`
  - Rationale: [why this matters]
  - Suggestion: [how to improve]

## Suggestions (consider for this PR or follow-up)

- [ ] [Suggestion] at `file:line`

## What's Done Well

- [Specific positive observation]
- [Another positive]

## Security Assessment

[Brief security posture of the changes]

## Performance Assessment

[Brief performance impact analysis]
```

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Reviews/YYYY-MM-DD-target.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/code-review.md

## Review Scope

$ARGUMENTS
