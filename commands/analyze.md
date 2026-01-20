---
description: Analyze a ticket and produce an implementation plan for /implement
argument-hint: "<ticket-id> - e.g., PROJ-123, bd-42, #123"
---

# Implementation Plan Analysis: $ARGUMENTS

## Prerequisites

Fetch the ticket details in full (JSON preferred) before proceeding.

---

## Step 1: Ticket Classification

After fetching the ticket:

1. Check if it's an **Epic** (type is epic, or has child tickets/dependents)
2. **If Epic:** Fetch all child tickets — these are the scope
3. **If Single Ticket:** This ticket alone is the scope

---

## Step 2: Codebase Research

Research the implementation context for each ticket in scope:

- Find relevant code locations
- Identify affected components
- Map dependencies and interfaces
- Note existing patterns to follow

**While researching, determine:**
- Implementation order based on dependencies
- Parallelization opportunities (which tickets can run concurrently)
- Shared concerns across tickets

---

## Step 3: Implementation Mapping

For each ticket, identify:

- Specific files to modify
- Functions/components to create or change
- Data model or schema changes
- Test files to add or update
- Verification approach

---

## Step 4: Output - Implementation Plan

Produce a structured implementation plan that `/implement` can execute.

### Plan Template

```markdown
# Implementation Plan: $ARGUMENTS

**Generated:** <timestamp>
**Ticket:** <title>
**Type:** Epic | Story | Task

## Executive Summary

[2-3 sentences: scope, approach, key decisions]

## Tickets in Scope

| ID  | Title | Status | Dependencies | Parallelizable |
| --- | ----- | ------ | ------------ | -------------- |
| ... | ...   | ...    | ...          | Yes/No         |

## Implementation Phases

### Phase 1: <name>

**Tickets:** <list of ticket IDs that can run in parallel>

#### Ticket <ID>: <title>

- **Work:**
  - [ ] <specific action>
  - [ ] <specific action>
- **Files:** <key files to modify>
- **Verification:** <how to verify completion>

### Phase 2: <name>

**Depends on:** Phase 1

[Continue for all phases]

## Parallel Execution Plan

```
Phase 1: [TICKET-1, TICKET-2] (parallel)
    |
    v
Phase 2: [TICKET-3] (depends on Phase 1)
    |
    v
Phase 3: [TICKET-4, TICKET-5, TICKET-6] (parallel)
```

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
| ---- | ---------- | ------ | ---------- |
| ...  | ...        | ...    | ...        |

## Discovered Gaps

If implementation analysis reveals missing prerequisites or undefined work:

| Gap | Description | Recommendation                                |
| --- | ----------- | --------------------------------------------- |
| ... | ...         | Run /story, create task, or proceed with risk |

**Note:** Gaps are blockers. Resolve before running /implement or acknowledge the risk.
```

---

## Step 5: Save Plan

Save the implementation plan to Obsidian:

- **Path:** `plans/$ARGUMENTS-plan.md`

---

## Quality Checklist

Before finalizing the plan:

- [ ] All tickets in scope are accounted for
- [ ] Dependencies are correctly mapped
- [ ] Parallelization opportunities identified
- [ ] Each ticket has specific file/code changes identified
- [ ] Verification criteria defined for each ticket
- [ ] Risks identified with mitigations
- [ ] Gaps flagged (if any)
- [ ] Plan saved to Obsidian

---

## Begin Analysis

Now analyze ticket: **$ARGUMENTS**

Start with Step 1: Fetch the ticket details.

**DO NOT IMPLEMENT ANY CODE**
**DO NOT CALL submit_plan** — this is analysis only. Save the plan to Obsidian, do not trigger interactive plan review.
