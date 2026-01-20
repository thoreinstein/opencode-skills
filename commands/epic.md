---
description: Refine an epic into high-level stories through cross-functional analysis
---

# Epic Refinement: $ARGUMENTS

## Prerequisites

Fetch the epic details in full (JSON preferred) before proceeding.

---

## 1. Cross-Functional Analysis

Analyze the epic through these lenses to identify gaps:

| Lens          | Key Questions                                                             |
| ------------- | ------------------------------------------------------------------------- |
| **Product**       | Are user value and scope boundaries clear? What user stories are missing? |
| **Architecture**  | Are system integration points, data flow, and contracts defined?          |
| **Quality/Risk**  | What are the failure modes? Is the acceptance criteria testable?          |
| **Data**          | Does this require schema changes, migrations, or new data models?         |
| **Observability** | What metrics, logs, and alerts are needed?                                |
| **Security**      | What auth, access control, or compliance requirements exist?              |
| **Performance**   | Are there latency, throughput, or scalability considerations?             |
| **ML/AI**         | Does this involve model training, inference, or data pipelines?           |

**Constraint:** DO NOT solution or implement code. Focus only on defining **what** needs to be built.

---

## 2. Output Format

### Part 1: Gap Analysis Report

* **Product Gaps:** [List findings]
* **Technical Gaps:** [List findings]
* **Data Implications:** [List findings]
* **Risk Factors:** [List findings]

### Part 2: Proposed Child Stories

| Story Title | User/Tech Goal           | Acceptance Criteria Summary |
| ----------- | ------------------------ | --------------------------- |
| [Title]     | [Who needs this and why] | [High level AC]             |

---

## 3. Story Creation

After completing the analysis and proposing stories:

1. Present the gap analysis and proposed stories for review
2. Once confirmed, create the stories as children of $ARGUMENTS using the project's work tracking tool

---

## Acceptance Criteria

- [ ] Epic analyzed through all relevant lenses
- [ ] Gap analysis report complete
- [ ] High-level stories identified (no implementation details)
- [ ] Stories created in work tracking system as children of $ARGUMENTS

**DO NOT IMPLEMENT ANY CODE**
