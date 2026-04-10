# claude-ops

A replicable, agent-driven project workflow system built on GitHub Issues and Claude Code.

<!-- ADD YOUR GOAL HERE — describe what this project is building or solving -->

---

## What This Is

claude-ops is a structured template for managing any project using AI agents, GitHub Issues, and a GitHub Project board. It provides a consistent ticket lifecycle, folder conventions, and a set of slash commands that agents can execute to create tickets, run research, build, and verify work.

This system is designed to be cloned and adapted to any domain — software, design, research, or otherwise.

---

## Workflow Overview

All work is organized into sprints and tracked as typed tickets:

| Type | Naming | Label |
|---|---|---|
| Bug | `BUG-{N}-{slug}` | `bug` |
| Work Order | `WO-{N}-{slug}` | `work-order` |

Each ticket lives under `.github/Sprint {N}/{TICKET-ID}-{slug}/` and contains:
- `ticket.md` — the ticket definition (synced to GitHub Issues)
- `plan.md` — implementation approach and step checklist
- `research/` — findings, data, reference docs
- `scripts/` — automation or helper scripts

**Lifecycle:** Draft locally → GitHub Issue → Project board → Plan → Work → Completed

---

## Slash Commands

| Command | What it does |
|---|---|
| `/create-ticket [bug\|wo] "[title]"` | Creates a ticket locally and syncs it to GitHub |
| `/research [Sprint N/TICKET-ID-slug] "[topic]"` | Runs a research agent on a ticket |
| `/figma-build [Sprint N/TICKET-ID-slug]` | Runs a Figma build agent on a ticket |
| `/vqa [Sprint N/TICKET-ID-slug]` | Runs a VQA pass and closes or recycles the ticket |
| `/project-start [project-name]` | Scaffolds this full workflow system in a new repo |

---

## Getting Started

1. Clone or fork this repo
2. Update the **Project Goal** in [`.github/templates/workflow.md`](.github/templates/workflow.md)
3. Update the **Project ID** and **Status field IDs** in `workflow.md` to match your GitHub Project board
4. Start creating tickets with `/create-ticket`

---

## Source of Truth

All agents operating in this repo should read [`.github/templates/workflow.md`](.github/templates/workflow.md) before starting any work.
