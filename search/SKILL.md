---
name: search
description: Deep search mode - parallel multi-source search across codebase, docs, and web
---

# DEEP SEARCH MODE

**Current Time:** !`date`

Execute a comprehensive search using parallel agent swarms across multiple sources.

## Search Protocol

### Layer 1: Local Codebase (Parallel)

Launch explore swarm with different angles:

```
background_task(agent="explore", prompt="Find [pattern] by filename...")
background_task(agent="explore", prompt="Find [pattern] in code content...")
background_task(agent="explore", prompt="Find related patterns and usages...")
```

Simultaneously use direct tools:

- `glob` — Find files by name pattern
- `grep` — Find content matches
- `ast_grep_search` — Find structural patterns
- `lsp_find_references` — Find symbol usages

### Layer 2: External Research (Parallel)

Launch librarian for external sources:

```
background_task(agent="librarian", prompt="Find official docs for [topic]...")
background_task(agent="librarian", prompt="Find OSS examples of [pattern]...")
```

Librarian searches:

- **Context7** — Official library documentation
- **grep.app** — GitHub code search across millions of repos
- **Exa** — Web search for blog posts, tutorials, discussions

### Layer 3: Deep Dive (As Needed)

For complex searches:

- Clone relevant repos for source analysis
- Check git history for evolution
- Search issues/PRs for context

## Search Output Format

```markdown
## Local Codebase Results

### Direct Matches

- `/path/to/file.go:42` — [why this matches]
- `/path/to/file.go:128` — [why this matches]

### Related Code

- `/path/to/related.go` — [how it's related]

### Patterns Found

[Describe any patterns or conventions discovered]

## External Resources

### Official Documentation

- [Link] — [what it covers]

### Code Examples

- [GitHub permalink] — [what this demonstrates]

### Articles/Tutorials

- [Link] — [relevance]

## Summary

[Synthesize findings: what was found, what's most relevant, what to do next]

## Recommended Next Steps

1. [Action based on findings]
```

## Search Strategies by Query Type

| Query Type             | Strategy                          |
| ---------------------- | --------------------------------- |
| "Where is X?"          | explore swarm + glob + grep       |
| "How does Y work?"     | explore + read key files + trace  |
| "Best practice for Z"  | librarian (context7 + exa)        |
| "Examples of W"        | librarian (grep.app + context7)   |
| "Why does V behave..." | explore + librarian + git history |

## Output

Write to Obsidian via `obsidian_append_content` at:
`$OBSIDIAN_PATH/Searches/YYYY-MM-DD-query.md`

> **Note**: `$OBSIDIAN_PATH` must be a vault-relative path (e.g., `Projects/myapp`), set per-project via direnv. The `obsidian_append_content` tool expects paths relative to the vault root.

### Document Structure

Use this template for the Obsidian document:

@~/.config/opencode/templates/search-results.md

## Search Query

$ARGUMENTS
