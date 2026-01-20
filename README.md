# Agent Skills Collection

A collection of reusable skills for AI coding agents, following the [Agent Skills Specification](https://agentskills.io/specification).

## What Are Agent Skills?

Agent Skills are modular, portable instruction sets that enhance AI coding assistants with specialized capabilities. Each skill defines:

- **When to use** - Trigger conditions and use cases
- **How to execute** - Step-by-step workflows and procedures
- **What tools are needed** - Required permissions and capabilities
- **Output format** - Templates and expected deliverables

Skills are agent-agnostic and can be used with any AI assistant that supports the specification.

## Available Skills

### Implementation & Development

| Skill | Description |
|-------|-------------|
| [implement](skills/implement/) | Full end-to-end feature implementation with phased execution, parallel work streams, and verification gates |
| [bugfix](skills/bugfix/) | Hypothesis-driven debugging with diagnostic instrumentation and evidence-based root cause identification |
| [debug](skills/debug/) | Systematic debugging through hypothesis generation and verification |
| [refactor](skills/refactor/) | Code analysis with blast radius assessment, risk evaluation, and recommended refactoring order |
| [enhance-frontend](skills/enhance-frontend/) | Frontend enhancement to pixel-perfect standards with mobile responsiveness |

### Analysis & Research

| Skill | Description |
|-------|-------------|
| [analyze](skills/analyze/) | Deep multi-phase investigation with expert consultation for complex problems |
| [research](skills/research/) | Codebase research to find and explain architecture, configuration, and implementation details |
| [ultrathink](skills/ultrathink/) | Ultra-deep multi-perspective analysis for complex architectural and strategic decisions |

### Code Quality

| Skill | Description |
|-------|-------------|
| [code-review](skills/code-review/) | Comprehensive code review with security, performance, and maintainability focus |
| [add-test-coverage](skills/add-test-coverage/) | Analyze recent changes and add test coverage for new code |
| [security-review](skills/security-review/) | Enterprise security review focusing on OWASP Top 10 and vulnerability analysis |

### Operations & Documentation

| Skill | Description |
|-------|-------------|
| [deploy-checklist](skills/deploy-checklist/) | Generate deployment checklists with pre-flight checks and rollout strategy |
| [runbook](skills/runbook/) | Generate operational runbooks with procedures, troubleshooting guides, and escalation paths |
| [commit](skills/commit/) | Analyze changes and suggest atomic commit groups with conventional commit messages |

### Writing & Content

| Skill | Description |
|-------|-------------|
| [content-writer](skills/content-writer/) | Research-driven content writing with citations, iterative outlines, and real-time feedback |

## Skill Structure

Each skill follows the Agent Skills Specification structure:

```
skills/
└── skill-name/
    ├── SKILL.md              # Main skill definition with frontmatter
    └── references/           # Supporting materials (optional)
        ├── detailed-guide.md
        └── templates/
            └── output-template.md
```

### SKILL.md Frontmatter

```yaml
---
name: skill-name
description: Brief description for agent discovery
license: MIT
compatibility:
  - runtime:any
  - vcs:git
allowed-tools:
  - Read
  - Write
  - Bash
metadata:
  author: thoreinstein
  version: 1.0.0
---
```

## Usage

### With Compatible Agents

Skills can be loaded by any agent that supports the Agent Skills Specification. The agent will:

1. Parse the SKILL.md frontmatter for metadata and permissions
2. Load the skill instructions into context
3. Follow the defined workflow when triggered

### Manual Reference

Skills can also be used as reference documentation for human developers following the same workflows.

## Contributing

Contributions are welcome! When adding or modifying skills:

1. Follow the [Agent Skills Specification](https://agentskills.io/specification)
2. Include comprehensive examples
3. Use the `references/` directory for lengthy supporting materials
4. Keep SKILL.md under 200 lines when possible
5. Test with at least one compatible agent

## License

MIT License - see [LICENSE](LICENSE) for details.

## Author

[thoreinstein](https://github.com/thoreinstein)
