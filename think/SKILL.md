---
name: think
description: Extended thinking mode - deep reasoning for complex problems requiring careful analysis
---

# DEEP THINKING MODE

**Current Time:** !`date`

This task requires extended reasoning. Take time to think through all aspects systematically before acting.

## Thinking Protocol

### Step 1: Problem Decomposition

Before solving, fully understand:

- What is the core problem?
- What are the constraints?
- What would success look like?
- What are the risks of getting it wrong?

### Step 2: Information Gathering

Gather necessary context:

```
background_task(agent="explore", prompt="Find relevant code for...")
background_task(agent="librarian", prompt="Research approaches for...")
```

Read key files directly to build mental model.

### Step 3: Alternative Analysis

Consider multiple approaches:

| Approach | Pros | Cons | Risk Level |
| -------- | ---- | ---- | ---------- |
| Option A |      |      |            |
| Option B |      |      |            |
| Option C |      |      |            |

For each, trace through:

- How would it work step by step?
- What could go wrong?
- How would we recover from failure?

### Step 4: Edge Case Exploration

Systematically consider:

- What if input is empty/null/invalid?
- What if operation times out?
- What if dependency fails?
- What about concurrent access?
- What about scale (10x, 100x, 1000x)?

### Step 5: Decision Framework

Choose approach based on:

1. **Correctness** — Does it solve the actual problem?
2. **Simplicity** — Is it the simplest solution that works?
3. **Robustness** — How does it handle failures?
4. **Maintainability** — Can others understand and modify it?
5. **Reversibility** — How hard to change if wrong?

### Step 6: Verification Strategy

Before implementing, plan verification:

- How will we know it works?
- What tests should exist?
- What manual verification is needed?
- What could we monitor in production?

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Thinking/YYYY-MM-DD-topic.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/thinking-session.md

## Thinking Principles

1. **Understand before solving** — Rushing to solution often misses the real problem
2. **Consider alternatives** — First idea isn't always best
3. **Trace through logic** — Walk through step by step
4. **Verify assumptions** — Question what you think you know
5. **Think about failure** — Happy path is easy; failure handling is hard
6. **Consider maintenance** — Someone else will read this code
7. **Simplify** — Can you remove anything?

## Think Deeply About

$ARGUMENTS
