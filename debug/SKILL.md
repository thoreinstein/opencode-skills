---
name: debug
description: Guide systematic debugging through hypothesis generation and verification
---

# Structured Debugging Workflow

**Current Time:** !`date`
**System:** !`uname -a`

Guide systematic debugging through hypothesis generation, investigation, and verification. Documents findings to Obsidian for knowledge retention.

## Input

- Problem statement: symptoms, error messages, reproduction steps
- Context: environment, recent changes, frequency
- Optional: initial hypotheses or suspected areas

## Investigation Strategy

Launch parallel investigation tracks:

### Track 1: Codebase Exploration (explore agent)

- Trace code paths related to error messages/symptoms
- Find error handling and logging in affected areas
- Identify recent changes to suspect code
- Map data flow through affected components

### Track 2: Code Analysis (inferred agent: go/frontend/postgres)

- Deep analysis of suspect code paths
- Identify potential failure modes
- Review error handling completeness
- Check for race conditions, edge cases, nil handling

### Track 3: External Research (librarian agent)

- Search for known issues matching error signatures
- Find similar bugs in dependency issue trackers
- Research common causes for the symptom pattern

## Debugging Framework

### 1. Problem Definition

- What is the expected behavior?
- What is the actual behavior?
- What changed recently?
- Is it reproducible? How?

### 2. Hypothesis Generation

Generate ranked hypotheses based on:

- Probability (how likely is this the cause?)
- Testability (how easy to verify/falsify?)
- Recent changes (correlation with deployments)
- Error signatures (what do the errors suggest?)

### 3. Investigation Plan

For each hypothesis:

- What evidence would confirm it?
- What evidence would refute it?
- What's the fastest way to test?

### 4. Evidence Collection

- Log analysis
- Metric correlation
- Code inspection
- Reproduction attempts
- Binary search (git bisect)

### 5. Root Cause Identification

- Distinguish symptoms from causes
- Identify contributing factors
- Verify fix addresses root cause

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Debugging/YYYY-MM-DD-HHMM-issue-title.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/debug-session.md

## Behavior

1. Parse problem statement to extract symptoms and context
2. Infer appropriate code agent from error context
3. Launch explore, librarian, and inferred code agent in parallel
4. Generate ranked hypotheses based on findings
5. Create investigation plan for top hypotheses
6. Document evidence and investigation log
7. Write debug session to Obsidian via `obsidian_append_content` with auto-generated filename: `YYYY-MM-DD-HHMM-issue-title.md`

$ARGUMENTS
