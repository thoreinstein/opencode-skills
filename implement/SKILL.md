---
name: implement
description: Full implementation mode - end-to-end feature implementation with parallel agent orchestration
---

# IMPLEMENTATION MODE

**Current Time:** !`date`
**Go Version:** !`go version`

Execute a complete feature implementation using coordinated agent swarms.

---

## MANDATORY: Roadmap Plugin Usage (NON-NEGOTIABLE)

You MUST use the roadmap plugin (`createroadmap`, `readroadmap`, `updateroadmap`) to:

1. **Define all phases BEFORE any implementation work begins**
2. **Track phase status** — mark `in_progress` when starting, `completed` when done
3. **Gate phase transitions** — do NOT proceed to next phase until current phase is committed
4. **Archive roadmap** — delete/archive when implementation is complete

---

## Phase Execution Loop (NON-NEGOTIABLE)

Every phase follows this exact sequence:

```
┌─────────────────────────────────────────────────────────────┐
│  PHASE EXECUTION LOOP                                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   1. PLAN     → Define work for this phase                  │
│                 Call: updateroadmap(status="in_progress")   │
│                                                             │
│   2. WORK     → Execute the phase work                      │
│                 Delegate to appropriate specialists         │
│                                                             │
│   3. VERIFY   → Run verification checklist                  │
│                 Tests pass, lints clean, build succeeds     │
│                                                             │
│   4. COMMIT   → Invoke commit skill                         │
│                 /commit (or load commit skill)              │
│                 Call: updateroadmap(status="completed")     │
│                                                             │
│   5. PROCEED  → Only after commit succeeds                  │
│                 Move to next phase                          │
│                                                             │
│   ⚠️  DO NOT PROCEED TO NEXT PHASE UNTIL COMMIT SUCCEEDS    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Implementation Protocol

### Phase 1: Requirements Analysis

**PLAN:** Gather context and define scope.

1. **Gather Context**

```
background_task(agent="explore", prompt="Find existing patterns for...")
background_task(agent="explore", prompt="Find related code that might be affected...")
background_task(agent="librarian", prompt="Research best practices for...")
```

2. **Clarify Requirements**

- What exactly needs to be built?
- What are the acceptance criteria?
- What constraints exist?
- What patterns should be followed?

3. **Create Roadmap (MANDATORY)**

Use `createroadmap` to define ALL phases with actions:

```
createroadmap(
  feature="Feature Name",
  spec="High-level specification...",
  features=[
    { number: "1", title: "Phase 1", description: "...", actions: [...] },
    { number: "2", title: "Phase 2", description: "...", actions: [...] },
    ...
  ]
)
```

Each phase MUST include a final action for commit:

```
{ number: "X.99", description: "Commit phase X changes via commit skill", status: "pending" }
```

**WORK:** N/A for this phase (planning only).

**VERIFY:** Roadmap created, requirements clear.

**COMMIT:** Use commit skill to commit any planning artifacts.

**PROCEED:** Only after commit succeeds.

---

### Phase 2: Architecture Decision (If Needed)

**PLAN:** Mark phase in_progress via `updateroadmap`.

**WORK:** For significant features, consult:

```
@architect Design the architecture for:
- [Feature description]
- Constraints: [list]
- Expected scale: [numbers]
```

Or for simpler decisions:

```
@principal Quick architecture gut check:
- [Approach description]
- [Alternative considered]
```

**VERIFY:** Architecture documented, decisions recorded.

**COMMIT:** Use commit skill to commit architecture docs/decisions.

**PROCEED:** Only after commit succeeds.

---

### Phase 3: Parallel Implementation

**PLAN:** Mark phase in_progress. Identify parallel work streams.

**WORK:** Deploy domain specialists in parallel where independent:

```
┌─────────────────────────────────────────────────────────────┐
│  PARALLEL IMPLEMENTATION SWARM                              │
├─────────────────────────────────────────────────────────────┤
│  BACKEND                     │  FRONTEND                    │
│  ├─ @go (Go APIs/CLIs)       │  └─ @frontend (UI)           │
│  ├─ @postgres (schema)       │                              │
│  ├─ @redis (redis)           │                              │
│  ├─ @gcp-dev (google apis)   │                              │
│  └─ @linux (shell scripts)   │                              │
├──────────────────────────────┼──────────────────────────────┤
│  INFRASTRUCTURE              │  QUALITY                     │
│  ├─ @k8s (manifests)         │  ├─ @testing (test strategy) │
│  ├─ @terraform (IaC)         │  ├─ @security (security)     │
│  ├─ @cicd (pipelines)        │  ├─ @perf (performance)      │
│  ├─ @nix (Nix configs)       │  ├─ @sre (reliability)       │
│  ├─ @finops (architecture)   │  ├─ @a11y (accessibility)    │
│  ├─ @gcp-architect (gcp)     │  ├─ @chaos (experiments)     │
│  └─ @security (entsec)       │  ├─ @o11y (observability)    │
│                              │  └─ @e2e (end to end tests)  │
└─────────────────────────────────────────────────────────────┘
```

**VERIFY:** All implementation work complete, tests written.

**COMMIT:** Use commit skill to commit all implementation changes.

**PROCEED:** Only after commit succeeds.

---

### Phase 4: Integration

**PLAN:** Mark phase in_progress.

**WORK:**

1. Integrate components
2. Resolve any conflicts
3. Ensure consistency across modules

**VERIFY:** Integration tests pass, no conflicts.

**COMMIT:** Use commit skill to commit integration changes.

**PROCEED:** Only after commit succeeds.

---

### Phase 5: Verification

**PLAN:** Mark phase in_progress.

**WORK:** Run full verification checklist:

```
┌─────────────────────────────────────────────────────────────┐
│  VERIFICATION CHECKLIST                                     │
├─────────────────────────────────────────────────────────────┤
│  [ ] lsp_diagnostics clean on all changed files             │
│  [ ] Tests pass (go test / npm test / etc.)                 │
│  [ ] Linter passes (golangci-lint / eslint)                 │
│  [ ] Build succeeds                                         │
│  [ ] Security review if needed (@security)                  │
│  [ ] Performance acceptable                                 │
└─────────────────────────────────────────────────────────────┘
```

**VERIFY:** All checks pass.

**COMMIT:** Use commit skill to commit any verification fixes.

**PROCEED:** Only after commit succeeds.

---

### Phase 6: Documentation & Cleanup

**PLAN:** Mark phase in_progress.

**WORK:**

- Update relevant documentation
- Clean up TODO list
- Cancel all background tasks
- Summarize what was implemented

**VERIFY:** Documentation complete, no orphaned tasks.

**COMMIT:** Use commit skill to commit documentation.

**CLEANUP (MANDATORY):**

- Archive or delete the roadmap file
- Mark all roadmap actions as completed via `updateroadmap`
- Confirm no uncommitted changes remain

---

## Implementation Output

At completion, provide:

```markdown
## Implementation Summary

### What Was Built

[Brief description of the feature]

### Files Changed

- `path/to/file.go` — [what changed]
- `path/to/file.go` — [what changed]

### Architecture Decisions

[Key decisions made and rationale]

### Testing

- [Tests added]
- [Coverage notes]

### Verification

- [ ] All diagnostics clean
- [ ] Tests passing
- [ ] Build succeeds

### Commits Made

- [Commit hash] — [Phase X: description]
- [Commit hash] — [Phase Y: description]

### Known Limitations

[Any constraints or future work]

### Next Steps

[Follow-up tasks if any]
```

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Implementations/YYYY-MM-DD-feature-name.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/implementation-summary.md

## Implement

$ARGUMENTS
