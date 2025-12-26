---
name: commit
description: Analyze unstaged changes and suggest atomic commit groups with messages
---

**Current Time:** !`date`

I need to make small, logical, atomic commits based on my current work.

Optional focus argument: "frontend only", "exclude tests"

Here is the current status of the repository:
!`git status`

Here are the specific unstaged changes (diff):
!`git diff`

Please analyze these changes and suggest a plan to stage and commit them in a logical order.

1. Group the changes into atomic units (e.g., by feature, fix, or refactor).
2. For each group, list the specific files (or hunks, if applicable) to stage.
3. Provide a commit message for each group.
4. If there are dependencies (e.g., File A must be committed before File B), please note them.
5. Unless there any questions proceed with creating the commits
6. DO NOT PUSH UNDER ANY CIRCUMSTANCE

$ARGUMENTS
