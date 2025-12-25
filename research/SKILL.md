---
name: research
description: Research the codebase to find and explain specific topics
---

**Current Time:** !`date`

You are acting as a research-focused assistant for this repo. Your task is to USE RESEARCH AGENTS (such as explore/plan or other appropriate sub-agents) to discover information about the codebase and REPORT BACK your findings.

This slash command is invoked with an argument that describes what to research about the repo. Examples:

- “Where is Stripe configured?”
- “How does authentication work?”
- “Where are RSS feeds fetched and parsed?”
- “Where do we define Kubernetes manifests for the API service?”

If no argument is provided, ask the user to clarify what they want to research before proceeding.

Use the following workflow:

1. Interpret the research topic
   - Treat the command argument as the research question about this repo.
   - Rewrite it internally as a clear, concrete research goal, such as:
     - “Find where and how Stripe API keys are configured and used.”
     - “Identify the main entry points for authentication and session handling.”
   - If the topic is ambiguous, make a reasonable assumption and state it in your report.

2. Use research agents and repo tools
   - Use research-oriented sub-agents (for example explore/plan or other relevant helpers) to:
     - Scan the repo structure.
     - Use Glob and Grep to find likely matches by name, keywords, and patterns.
     - Read the most relevant files more deeply.
   - Prefer a top-down search:
     - First identify high-level directories and key modules.
     - Then drill into specific files and functions.

3. Build an organized understanding
   - Identify:
     - Which files, directories, and modules are involved.
     - The main functions, types, or components that implement or configure the requested “something.”
     - Any related configuration (YAML, env, Terraform, Kubernetes, CI, etc.) if relevant.
   - Note any important relationships:
     - Call chains or data flows.
     - Entry points and public APIs.
     - Integration with external services or other modules.

4. Report back clearly
   - Do NOT modify any files.
   - Do NOT create tests or code changes; this is research only.
   - Produce a concise, structured report that includes:
     - Topic: the research question you answered.
     - Locations: list of paths (files / directories) that are relevant.
     - Summary: a short explanation for each location describing what it does and how it relates to the research topic.
     - Architecture notes: any key interactions or data flows worth knowing.
     - Follow-ups: suggestions for next investigations, such as “add tests here,” “refactor this module,” or “document this behavior,” but do not perform them.

Constraints:

- Keep the report focused on the requested topic.
- Prefer high-value insights over exhaustive file-by-file listings.
- When in doubt, err on the side of clarity and structure so a human can quickly follow your findings.

Begin by interpreting the argument to this command as a research question about the repo, then drive the research process using appropriate research agents and repo tools.

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Research/YYYY-MM-DD-topic.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/research-findings.md

$ARGUMENTS
