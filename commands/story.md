---
description: Refine a story into technical tasks through implementation analysis
---

# Story Refinement: $ARGUMENTS

## Prerequisites

Fetch the story details in full (JSON preferred) before proceeding.

---

## 1. Implementation Analysis

Analyze the story through these lenses to identify implementation gaps:

| Lens             | Key Questions                                                                |
| ---------------- | ---------------------------------------------------------------------------- |
| **Edge Cases**       | Are error states, empty states, and permission checks defined?               |
| **Component Design** | Which specific files, functions, or API endpoints need modification?         |
| **Testing**          | What unit tests, integration tests, or manual verification steps are needed? |
| **Data**             | Are the specific field types, validations, and query patterns defined?       |
| **Observability**    | Do we need new log lines, metrics, or traces for this feature?               |
| **Security**         | Are there input validation, auth, or access control requirements?            |
| **Performance**      | Are there caching, pagination, or optimization considerations?               |

**Constraint:** DO NOT write code. Focus on defining **technical tasks** required to complete this story.

---

## 2. Output Format

### Part 1: Implementation Gaps

* **Missing Edge Cases:** [List findings]
* **Technical Complexity:** [List findings]
* **Verification Gaps:** [List findings]

### Part 2: Proposed Technical Tasks

| Task Title | Technical Goal          | Verification Criteria |
| ---------- | ----------------------- | --------------------- |
| [Title]    | [What needs to be done] | [How to verify]       |

---

## 3. Task Creation

After completing the analysis and proposing tasks:

1. Present the implementation gaps and proposed tasks for review
2. Once confirmed, create the tasks as children of $ARGUMENTS using the project's work tracking tool

---

## Acceptance Criteria

- [ ] Story analyzed through all implementation lenses
- [ ] Implementation gaps report complete
- [ ] Technical tasks identified with clear verification criteria
- [ ] Tasks created in work tracking system as children of $ARGUMENTS

**DO NOT IMPLEMENT ANY CODE**
