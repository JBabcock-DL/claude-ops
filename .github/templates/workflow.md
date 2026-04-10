# claude-ops — Agent Workflow Context

This document describes how this project is structured and how work is tracked. All agents operating in this repo should follow this workflow.

---

## Project Goal

Build a design system visual guide in Figma and manage all work through GitHub Issues synced to the **Process Demo** GitHub Project board.

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
3. **Sync to Project** — add the issue to the **Process Demo** project board (`gh project item-add`)
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

## Figma Integration

Figma work is driven by tickets. Each work order that involves canvas changes should:
- Reference the Figma file URL in `ticket.md` under **References**
- Document what was built or changed in `plan.md` after completion
- The Figma MCP (`mcp__claude_ai_Figma__*`) is available for reading designs, writing to canvas, and managing variables

---

## Conventions

- Ticket IDs are sequential per type (`BUG-001`, `BUG-002`, `WO-001`, `WO-002`)
- Sprint folders are named `Sprint {N}` — do not use dates
- All `ticket.md` files include a `github_issue` frontmatter field linking to the GitHub issue number
- `plan.md` is always a stub when first created — fill it in before starting work
