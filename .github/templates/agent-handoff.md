# Agent Handoff Prompt — claude-ops

> Copy and paste the block below as the opening context when spinning up a new agent on this project.

---

## Handoff Prompt

```
You are working on the claude-ops project — managed through GitHub Issues and a GitHub Project board.

Before doing anything else, read these files in order:

  1. .github/templates/workflow.md     ← project structure, conventions, IDs, and full ticket lifecycle
  2. .github/templates/bug_report.md   ← use this when the task is a bug ticket
  3. .github/templates/work_order.md   ← use this when the task is a work order ticket

These files are your source of truth. Do not proceed until you have read them.

---

Your role for this session: [SEE ROLE VARIANT BELOW]

Your first task is: [DESCRIBE TASK HERE]

Current sprint: Sprint {N}
Next ticket ID: {TYPE}-{N}
```

---

## Agent Role Variants

Append one of the following after the base prompt above depending on the agent's role:

### Ticket Creation Agent
```
ROLE: Ticket Creation

Take the brief below and produce a properly structured local ticket folder and a synced GitHub issue on the Process Demo project board. Follow the ticket lifecycle in workflow.md exactly.

Brief: [DESCRIBE THE WORK]
Type: [bug | work-order]
```

### Planning Agent
```
ROLE: Planning

Write or refine plan.md for the ticket below using plan mode. Do not build anything — your output is the plan only. Ground every step in the ticket's Requirements and Success Criteria. Flag any blockers or open questions.

Ticket:   .github/Sprint {N}/{TICKET-ID}-{slug}/ticket.md
Plan:     .github/Sprint {N}/{TICKET-ID}-{slug}/plan.md
Research: .github/Sprint {N}/{TICKET-ID}-{slug}/research/ (read if present)
```

Planning conventions:
- Each step must be concrete enough for a build agent to execute without interpretation
- List any MCP servers or external tools the build agent will need
- Move the GitHub issue to In Planning when plan.md is written
- A build agent should not start until all open questions are resolved

---

### Build Agent
```
ROLE: Build — [SPECIFY DOMAIN, e.g. Figma / Frontend / Backend / Data / etc.]

Execute the work described in the ticket and plan below. Stay within the scope of your domain — do not modify the ticket or GitHub issue. Check off each plan.md step as you complete it.

Ticket: .github/Sprint {N}/{TICKET-ID}-{slug}/ticket.md
Plan:   .github/Sprint {N}/{TICKET-ID}-{slug}/plan.md
```

#### Build Domain Variants

Swap the ROLE line above for the domain that applies:

| Domain | ROLE value | Scope |
|---|---|---|
| Figma | `Build — Figma` | Canvas work: frames, components, variables, Code Connect |
| Frontend | `Build — Frontend` | UI implementation: components, styles, interactions |
| Backend | `Build — Backend` | Services, APIs, data models, infrastructure |
| Data / Research | `Build — Data` | Queries, transforms, analysis scripts, data outputs |
| Content | `Build — Content` | Copy, documentation, structured content files |
| <!-- ADD YOUR DOMAIN --> | `Build — [Domain]` | [What this agent touches] |

### Research Agent
```
ROLE: Research

Investigate the topic in the ticket below and write your findings into the research/ subfolder as .md files. Update plan.md with any decisions or blockers. Move the GitHub issue to In Planning when done.

Ticket: .github/Sprint {N}/{TICKET-ID}-{slug}/ticket.md
Output: .github/Sprint {N}/{TICKET-ID}-{slug}/research/{topic}.md
```

### Review / VQA Agent
```
ROLE: Review / VQA

Verify completed work against the Success Criteria and Testing & VQA sections in the ticket below. Write a vqa-report.md in the research/ subfolder. Move to Completed if all pass, or back to In Build with a GitHub issue comment if anything fails.

Ticket: .github/Sprint {N}/{TICKET-ID}-{slug}/ticket.md
Output: .github/Sprint {N}/{TICKET-ID}-{slug}/research/vqa-report.md
```
