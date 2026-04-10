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
| 4 | `/build [Sprint N/TICKET-ID-slug]` | Orchestrates all build agents in parallel phases — preferred entry point for the build step |
| 4 | `/code-build [Sprint N/TICKET-ID-slug]` | Run individually if only code work is needed |
| 4 | `/doc-build [Sprint N/TICKET-ID-slug]` | Run individually if only doc work is needed |
| 4 | `/script-build [Sprint N/TICKET-ID-slug]` | Run individually if only scripting is needed |
| 4 | `/api-build [Sprint N/TICKET-ID-slug]` | Run individually if only API work is needed |
| 4 | `/figma-build [Sprint N/TICKET-ID-slug]` | Run individually if only Figma work is needed |
| 5 | `/vqa [Sprint N/TICKET-ID-slug]` | Runs a VQA pass and closes or recycles the ticket |
| — | `/project-start [project-name]` | Scaffolds this full workflow system in a new repo |

## Key Conventions

- All work is organized under `.github/Sprint {N}/` — never create tickets outside a sprint folder
- Preferred order: research → plan → build → vqa; skip research only for mechanical, well-understood tickets
- Every ticket has a `ticket.md` and a `plan.md` — the plan must be written and approved before build starts
- GitHub issues and project board are the canonical source of ticket status
- MCP-driven work (Figma, or other integrations) is always tied to a work order ticket
