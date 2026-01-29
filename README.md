# Note-Driven Agentic Coding Workflow

> Store Claude Code plans in Inkdrop for better readability and progress tracking

This is a fork of [everything-claude-code](https://github.com/affaan-m/everything-claude-code) that integrates with [Inkdrop](https://www.inkdrop.app/), a markdown note-taking app, to persist plans and track execution progress.

## Why Note-Driven?

When Claude Code creates a plan, it displays in the terminal. But terminal output is hard to read for complex plans with multiple phases, code snippets, and detailed steps.

By storing plans in Inkdrop, you get:

- **Beautiful markdown rendering** - Plans are much easier to read with proper formatting, syntax highlighting, Mermaid diagrams, and LaTeX math blocks
- **Easy to edit** - Modify the plan before confirming, add notes, or adjust steps directly with the robust Markdown editor in Inkdrop
- **Multi-device review** - Review and approve plans from any device, including your phone
- **Revision history** - Track exactly when work started, what changed, and when it completed, with [Inkdrop's revision history](https://docs.inkdrop.app/reference/revision-history)
- **Progress tracking** - Watch checkboxes get ticked off and status updates appear in real-time

## How It Works

1. **Request a plan** - Run the `/plan` command with your task description
2. **Plan is created** - Claude Code analyzes the codebase and generates a detailed implementation plan
3. **Saved to Inkdrop** - The plan is automatically saved as a note with status `none`
4. **Review and confirm** - Read the plan in Inkdrop's markdown renderer, then confirm to proceed
5. **Execution begins** - Status changes to `active`, work starts
6. **Progress updates** - Checkboxes are checked off, deviations annotated, blockers noted
7. **Completion** - Status changes to `completed`, outcome section appended

### Note Format

Plans are stored with YAML frontmatter containing:

```yaml
---
projectDir: /path/to/your/project
description: Brief summary of what the plan accomplishes
gitBranch: feature-branch (optional)
---
```

### Status Lifecycle

| Status      | Meaning                             |
| ----------- | ----------------------------------- |
| `none`      | Plan created, awaiting confirmation |
| `active`    | Work in progress                    |
| `completed` | Successfully finished               |
| `onHold`    | Blocked or paused                   |
| `dropped`   | Abandoned                           |

### Inkdrop Features Used

Plans can include:

- **Codeblock attributes** - Show line numbers, filenames, commit hashes, and URLs
- **Mermaid diagrams** - Visualize architecture and flow
- **LaTeX math** - Document algorithms and calculations

See [`commands/plan.md`](commands/plan.md) for syntax examples.

## What This Fork Adds

This fork modifies three files from the original repository:

| File                   | Change                                        |
| ---------------------- | --------------------------------------------- |
| `rules/note-taking.md` | **NEW** - Core rules for Inkdrop integration  |
| `agents/planner.md`    | Added `mcp__inkdrop__*` tools for note access |
| `commands/plan.md`     | Added Inkdrop codeblock syntax tips           |

## Getting Started

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI installed
- [Inkdrop](https://www.inkdrop.app/) - v5 or v6
- [Inkdrop MCP server](https://github.com/inkdropapp/mcp-server) configured

### Installation

1. **Set up the Inkdrop MCP server** following the [instructions](https://github.com/inkdropapp/mcp-server)
2. **Copy the rule file** to your Claude Code rules directory:

   ```bash
   cp rules/note-taking.md ~/.claude/rules/
   ```

3. **Copy the modified agent and command** (optional, for enhanced planning):
   ```bash
   cp agents/planner.md ~/.claude/agents/
   cp commands/plan.md ~/.claude/commands/
   ```

### Configuration

Edit `rules/note-taking.md` and update the notebook name to match your Inkdrop setup:

```markdown
Store notes in the notebook `<NODEBOOK_NAME>`.
```

If you'd like to specify by notebook ID instead, use the [dev-tools](https://my.inkdrop.app/plugins/dev-tools) plugin to quickly copy the ID.
You can find your notebook ID in Inkdrop's developer tools or by using the MCP server's `list-notebooks` tool.

## Directory Structure

This fork maintains the same structure as the original. Key directories:

```
agents/      # Specialized subagents (planner modified for Inkdrop)
commands/    # Slash commands (/plan modified for Inkdrop)
rules/       # Always-follow guidelines (note-taking.md added)
skills/      # Workflow definitions
hooks/       # Trigger-based automations
```

See the [original repository](https://github.com/affaan-m/everything-claude-code) for the complete structure and documentation.

## Credits

This project is a fork of [everything-claude-code](https://github.com/affaan-m/everything-claude-code) by [Affaan Mustafa](https://github.com/affaan-m), winner of the Anthropic Hackathon.
The original repository provides production-ready Claude Code configurations developed over 10+ months of intensive use.

## Related Resources

- [everything-claude-code](https://github.com/affaan-m/everything-claude-code) - Original repository
- [Inkdrop](https://www.inkdrop.app/) - Markdown note-taking app
- [Inkdrop MCP Server](https://github.com/inkdropapp/mcp-server) - MCP server for Inkdrop integration
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code) - Official docs
