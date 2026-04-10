# claude-ops — Claude Context

This project uses a structured workflow for managing design system work across Figma and GitHub. Before starting any work, read the source of truth:

  .github/templates/workflow.md

## Skills Available

These slash commands are available in this project:

| Command | What it does |
|---|---|
| `/create-ticket [bug\|wo] "[title]"` | Creates a ticket locally and syncs it to GitHub |
| `/figma-build [Sprint N/TICKET-ID-slug]` | Runs a Figma build agent on a ticket |
| `/research [Sprint N/TICKET-ID-slug] "[topic]"` | Runs a research agent on a ticket |
| `/vqa [Sprint N/TICKET-ID-slug]` | Runs a VQA pass and closes or recycles the ticket |
| `/project-start [project-name]` | Scaffolds this full workflow system in a new repo |

## Key Conventions

- All work is organized under `.github/Sprint {N}/` — never create tickets outside a sprint folder
- Every ticket has a `ticket.md` and a `plan.md` — write the plan before starting work
- GitHub issues and project board are the canonical source of ticket status
- Figma work is always tied to a work order ticket
