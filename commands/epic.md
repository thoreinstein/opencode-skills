---
description: Refine an epic into high-level stories through cross-functional analysis
---

# Epic Refinement: $ARGUMENTS

## HARD CONSTRAINTS (NON-NEGOTIABLE)

- **NO CODE READING** — Do not read, analyze, or reference source code. This is a requirements refinement exercise.
- **NO SOLUTIONING** — Do not propose technical implementations, architecture decisions, or design patterns.
- **NO IMPLEMENTATION DETAILS** — Stories must describe WHAT, never HOW.
- **DO NOT CALL submit_plan** — This is a discussion, not a plan-and-implement cycle.

If you find yourself wanting to look at code, STOP. Return to the epic description and acceptance criteria.

---

## Prerequisites

Fetch the epic details in full (JSON preferred) before proceeding:
- For beads: `bd show $ARGUMENTS --json`

---

## 1. Epic Description & AC Refinement

Before creating child stories, ensure the epic itself is well-defined:

| Check                   | Question                                                             |
| ----------------------- | -------------------------------------------------------------------- |
| **Clear Problem Statement** | Does the description explain the user/business problem being solved? |
| **Scope Boundaries**        | Is it clear what is IN and OUT of scope?                             |
| **User Value**              | Is the value proposition explicit?                                   |
| **Testable AC**             | Can each acceptance criterion be verified without ambiguity?         |
| **Dependencies**            | Are external dependencies or prerequisites noted?                    |

**Output:** List any gaps or ambiguities in the epic that need clarification before proceeding.

---

## 2. Cross-Functional Gap Analysis

Analyze the epic through these lenses to identify what's missing from requirements (NOT solutions):

| Lens          | Key Questions                                                            |
| ------------- | ------------------------------------------------------------------------ |
| **Product**       | Are user personas and their goals clear? What user journeys are implied? |
| **Data**          | What data inputs/outputs are implied? Any data ownership questions?      |
| **Quality/Risk**  | What could go wrong? What edge cases need consideration?                 |
| **Security**      | What access control or compliance requirements exist?                    |
| **Observability** | What does "success" look like? How will we know it's working?            |

**Output:** Gap Analysis Report
- **Clarifications Needed:** [Questions for product/stakeholders]
- **Missing Requirements:** [Gaps in the epic definition]
- **Risk Factors:** [Unknowns that could affect scope]

---

## 3. Propose Child Stories

Break the epic into discrete, deliverable stories. Each story should be:
- **User-focused** — Describes value, not implementation
- **Independently deliverable** — Can be completed and verified on its own
- **Small enough** — Can be refined further in `/story`

| Story Title | User/Business Goal     | High-Level AC        |
| ----------- | ---------------------- | -------------------- |
| [Title]     | [Who benefits and why] | [Verifiable outcome] |

---

## 4. Review & Create Stories

1. **Present for confirmation** — Show the gap analysis and proposed stories to the user
2. **Wait for explicit approval** — Do not create stories until user confirms
3. **Create child stories** in the project's work tracking system

**For projects using beads:**
```bash
bd create "<story title>" --parent=$ARGUMENTS
```
**MANDATORY for beads projects:** Every child story MUST include `--parent=$ARGUMENTS` to establish the hierarchy.

If stories have dependencies on each other:
```bash
bd dep add <story-id> <blocked-by-id>
```

**For projects using other tracking systems (GitHub Issues, Jira, etc.):**
- Create stories as children/sub-issues of the parent epic
- Ensure parent-child relationship is established per that system's conventions

---

## Acceptance Criteria

- [ ] Epic description and AC reviewed for clarity and completeness
- [ ] Gap analysis identifies missing requirements (not solutions)
- [ ] Child stories are user-focused stubs (no implementation details)
- [ ] All stories created with proper parent linkage (beads: `--parent=$ARGUMENTS`)
- [ ] No code was read or referenced during this process
