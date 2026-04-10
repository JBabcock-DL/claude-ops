# claude-ops — Claude Context

This project uses a structured workflow for managing work across tools and GitHub. Before starting any work, read the source of truth:

  .github/templates/workflow.md

## Skills Available

These slash commands are available in this project. Run them in order:

| Step | Command | What it does |
|---|---|---|
| 1 | `/create-ticket [bug\|wo] "[title]"` | Creates a ticket locally and syncs it to GitHub |
| 2 | `/research [Sprint N/TICKET-ID-slug] "[topic]"` | Runs a research agent on a ticket *(optional)* |
| 3 | `/plan [Sprint N/TICKET-ID-slug]` | Writes plan.md using plan mode — presents for review before saving |
| 4 | `/code-build [Sprint N/TICKET-ID-slug]` | Implements code changes defined in plan.md |
| 4 | `/doc-build [Sprint N/TICKET-ID-slug]` | Writes documentation defined in plan.md |
| 4 | `/script-build [Sprint N/TICKET-ID-slug]` | Writes automation or shell scripts defined in plan.md |
| 4 | `/api-build [Sprint N/TICKET-ID-slug]` | Builds API integrations or Claude API features defined in plan.md |
| 4 | `/figma-build [Sprint N/TICKET-ID-slug]` | Executes Figma canvas work defined in plan.md |
| 5 | `/vqa [Sprint N/TICKET-ID-slug]` | Runs a VQA pass and closes or recycles the ticket |
| — | `/project-start [project-name]` | Scaffolds this full workflow system in a new repo |

## Key Conventions

- All work is organized under `.github/Sprint {N}/` — never create tickets outside a sprint folder
- Preferred order: research → plan → build → vqa; skip research only for mechanical, well-understood tickets
- Every ticket has a `ticket.md` and a `plan.md` — the plan must be written and approved before build starts
- GitHub issues and project board are the canonical source of ticket status
- MCP-driven work (Figma, or other integrations) is always tied to a work order ticket
