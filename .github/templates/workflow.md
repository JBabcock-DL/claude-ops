# claude-ops — Agent Workflow Context

This document describes how this project is structured and how work is tracked. All agents operating in this repo should follow this workflow.

---

## Project Goal

<!-- ADD YOUR GOAL HERE — describe what this project is building or solving -->
[ADD YOUR GOAL HERE]

All work is managed through GitHub Issues synced to the **claude-ops** GitHub Project board.

---

## Repository Structure

```
.github/
├── templates/               # Ticket templates and agent workflow context
│   ├── workflow.md          # This file — agent context document
│   ├── bug_report.md        # Template for bug tickets
│   └── work_order.md        # Template for feature/work order tickets
└── Sprint {N}/              # One folder per sprint
    └── {TICKET-ID}-{slug}/  # One folder per ticket
        ├── ticket.md        # The ticket definition (synced to GitHub Issues)
        ├── plan.md          # Implementation approach and step checklist
        ├── research/        # Data, findings, reference docs (.md, .json, etc.)
        └── scripts/         # Any automation, tooling, or helper scripts
```

---

## Ticket Types

| Type | Label | Template | Naming |
|---|---|---|---|
| Bug | `bug` | `bug_report.md` | `BUG-{N}-{slug}` |
| Work Order | `work-order` | `work_order.md` | `WO-{N}-{slug}` |

---

## Ticket Lifecycle

1. **Draft locally** — create a folder under the current sprint using the ticket ID and slug, add `ticket.md` from the appropriate template
2. **Create GitHub Issue** — push the ticket to GitHub using `gh issue create`, referencing the correct label
3. **Sync to Project** — add the issue to the **claude-ops** project board (`gh project item-add`)
4. **Add a plan** — create `plan.md` in the ticket folder outlining approach and steps
5. **Do the work** — place any scripts, data, or research files inside the ticket folder
6. **Move to Completed** — update the project board status when the work is done

---

## GitHub Project

- **Project name:** Process Demo
- **Project ID:** `PVT_kwHOD9B30s4BTj7z`
- **Owner:** `JBabcock-DL`
- **Status field ID:** `PVTSSF_lAHOD9B30s4BTj7zzhAyGKQ`

### Status Options

| Status | Option ID |
|---|---|
| Context Backlog | `f75ad846` |
| In Research | `61e4505c` |
| In Planning | `47fc9ee4` |
| In Build | `df73e18b` |
| In Verification | `98236657` |
| Completed | `209a9b95` |

---

## Key Commands

```bash
# Create a GitHub issue
gh issue create --repo JBabcock-DL/claude-ops --title "..." --label "..." --body "..."

# Add issue to project board
gh project item-add 1 --owner JBabcock-DL --url https://github.com/JBabcock-DL/claude-ops/issues/{N}

# Move issue to a status column
gh api graphql -f query='
mutation {
  updateProjectV2ItemFieldValue(input: {
    projectId: "PVT_kwHOD9B30s4BTj7z"
    itemId: "{PVTI_...}"
    fieldId: "PVTSSF_lAHOD9B30s4BTj7zzhAyGKQ"
    value: { singleSelectOptionId: "{option-id}" }
  }) {
    projectV2Item { id }
  }
}'

# List issues in the project
gh project item-list 1 --owner JBabcock-DL
```

---

## MCP Integrations

MCP (Model Context Protocol) servers extend what agents can do within this workflow — connecting to external tools, APIs, and platforms without leaving the ticket lifecycle. Any MCP-driven work should still be tied to a ticket.

### General conventions for MCP work
- Reference any external resource URLs (files, boards, APIs) in `ticket.md` under **References**
- Document what was read, written, or changed via MCP in `plan.md` after completion
- MCP tool calls are treated as implementation steps — they belong in the work phase, after a plan exists

### Available MCP servers

#### Figma (`mcp__claude_ai_Figma__*`)
Read designs, write to the Figma canvas, manage variables and component code connections.

Use when a work order involves:
- Reading a Figma design to inform implementation
- Writing components, frames, or variables back to a Figma file
- Generating diagrams in FigJam
- Managing Code Connect mappings between Figma and the codebase

<!-- ADD YOUR MCP SERVERS HERE
#### [Server Name] (`mcp__<server>__*`)
Brief description of what it connects to and what it can do.

Use when a work order involves:
- ...
-->

---

## Conventions

- Ticket IDs are sequential per type (`BUG-001`, `BUG-002`, `WO-001`, `WO-002`)
- Sprint folders are named `Sprint {N}` — do not use dates
- All `ticket.md` files include a `github_issue` frontmatter field linking to the GitHub issue number
- `plan.md` is always a stub when first created — fill it in before starting work
