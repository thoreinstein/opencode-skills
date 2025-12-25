---
name: analyze
description: Deep analysis mode - thorough multi-phase investigation with expert consultation
---

# DEEP ANALYSIS MODE

**Current Time:** !`date`

Perform a comprehensive analysis using multi-phase expert consultation and parallel research.

## Analysis Protocol

### Phase 1: Reconnaissance (Parallel Swarm)

Launch immediately:

```
background_task(agent="explore", prompt="Map relevant code structure...")
background_task(agent="explore", prompt="Find related patterns...")
background_task(agent="librarian", prompt="Research best practices for...")
```

While swarm runs, use direct tools:

- `glob` to find relevant files
- `grep` to identify patterns
- `read` to understand key code

### Phase 2: Expert Analysis

Based on findings, consult specialists:

| Domain       | Agent        | Focus                                   |
| ------------ | ------------ | --------------------------------------- |
| Architecture | `@architect` | System design, data flow, dependencies  |
| Security     | `@security`  | Vulnerabilities, threat model, risks    |
| Reliability  | `@sre`       | Scalability, SLOs, observability        |
| Performance  | `@perf`      | Profiling, bottlenecks, optimization    |
| Patterns     | `@principal` | Code quality, best practices, tradeoffs |

### Phase 3: Deep Dive

Analyze comprehensively:

- Edge cases and potential failure modes
- Performance implications under load
- Security attack surface
- Error handling completeness
- Testability and maintainability
- Technical debt assessment

### Phase 4: Synthesis

Combine findings into actionable output:

```markdown
## Executive Summary

[2-3 sentences: key findings and recommendation]

## Detailed Analysis

### Architecture

[Component analysis, data flow, dependencies]

### Code Quality

[Patterns, anti-patterns, maintainability]

### Security

[Vulnerabilities, risks, compliance]

### Performance

[Bottlenecks, scalability concerns]

## Issues Found

### Critical (P0)

- [Issue with location and impact]

### High (P1)

- [Issue]

### Medium (P2)

- [Issue]

## Recommendations

### Immediate Actions

1. [Action with rationale]

### Short-term Improvements

1. [Improvement]

### Long-term Considerations

1. [Consideration]

## Trade-offs

[Analysis of different approaches with pros/cons]
```

## Analysis Focus Areas

| Area                | What to Examine                         |
| ------------------- | --------------------------------------- |
| **Correctness**     | Logic errors, edge cases, assumptions   |
| **Security**        | Input validation, auth, data protection |
| **Performance**     | Complexity, caching, resource usage     |
| **Reliability**     | Error handling, failure modes, recovery |
| **Maintainability** | Readability, coupling, documentation    |
| **Testability**     | Coverage, mocking, isolation            |

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Analysis/YYYY-MM-DD-target.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/analysis-report.md

## Analyze

$ARGUMENTS
