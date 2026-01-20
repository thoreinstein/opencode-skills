---
description: Execute an implementation plan with phase-gated commits
argument-hint: "<ticket-id> - must have a plan from /analyze"
---

# Implementation: $ARGUMENTS

## Prerequisites

1. Fetch the ticket details
2. Load the implementation plan from Obsidian: `plans/$ARGUMENTS-plan.md`

If no plan exists, run `/analyze $ARGUMENTS` first.

---

## Status Update

Mark the ticket as **in progress** before beginning implementation.

---

## Phase Execution Loop

Execute each phase from the implementation plan following this exact sequence:

```
Plan → Work → Verify → Commit → Proceed
```

### For Each Phase:

#### 1. Plan
- Review the phase scope from the implementation plan
- Identify the specific tickets/tasks in this phase
- Mark each task as in progress

#### 2. Work
- Execute the implementation work
- Follow existing codebase patterns
- Delegate to specialists as needed (tests, security review, etc.)

#### 3. Verify
- Run tests relevant to the changes
- Run lints and type checks
- Verify acceptance criteria are met
- Ensure no regressions

#### 4. Commit
- Invoke `/commit` to stage and commit the phase work
- Include ticket ID in commit message for traceability

```
⚠️  DO NOT PROCEED TO NEXT PHASE UNTIL COMMIT SUCCEEDS
```

If commit fails, fix issues and retry. Never advance with uncommitted work.

#### 5. Proceed
- Mark completed tasks as done
- Move to the next phase

---

## Final Cleanup

After the last phase:

- Verify all tasks are marked complete
- Confirm no uncommitted changes remain
- Mark the ticket as complete/done

---

## Traceability

Throughout implementation:
- Keep ticket ID visible in reasoning and summaries
- Include ticket ID in commit messages and branch names
- If you discover out-of-scope work, note it as follow-up — do not expand scope

---

## Begin Implementation

Now implement ticket: **$ARGUMENTS**

Start by fetching the ticket and loading the plan.
