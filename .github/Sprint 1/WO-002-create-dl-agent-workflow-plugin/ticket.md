---
id: WO-002
title: Create DL-Agent-Workflow Claude Code Plugin
type: work-order
sprint: 1
status: In Research
github_issue: 4
project_item_id: PVTI_lAHOD9B30s4BTj7zzgponuA
---

## Problem Story

As a DL team member, I need the DL-Agent-Workflow packaged as a Claude Code plugin so that the full agent workflow system — skills, templates, and conventions — can be installed and used directly inside Claude Code without manual setup.

## Hypothesis

We believe that distributing DL-Agent-Workflow as a Claude Code plugin will allow team members to adopt the workflow in any repo with minimal friction. We'll know we're right when a team member can install the plugin and have all slash commands (skills) available in Claude Code within minutes of setup.

## Requirements

- [ ] Assemble plugin directory at `plugin/` with `.claude-plugin/plugin.json` metadata, `skills/` (6 skills), and `templates/` (4 templates) matching the standard Claude Code plugin structure
- [ ] Confirm and document the exact `.claude-plugin/plugin.json` schema (required fields: name, version, description, skills list)
- [ ] All 6 skills (`create-ticket`, `research`, `plan`, `figma-build`, `vqa`, `project-start`) packaged under `plugin/skills/` as SKILL.md files using `agent: general-purpose`
- [ ] All 4 templates (`workflow.md`, `bug_report.md`, `work_order.md`, `agent-handoff.md`) packaged under `plugin/templates/`
- [ ] Write `plugin/install.sh` (Unix) and `plugin/install.ps1` (Windows) that copy the plugin tree into a target repo's `.claude/` and `.github/templates/`, with a `--force` flag for overwriting
- [ ] Write `plugin/INSTALL.md` covering: prerequisites (`gh` CLI, `git`, Claude Code), install commands per platform, and post-install steps (configure GitHub Project IDs in `workflow.md`)
- [ ] Write `plugin/README.md` with plugin overview, full skills table with one-line descriptions, and link to `INSTALL.md`

## Success Criteria

- [ ] Plugin installs correctly in Claude Code from a clean state
- [ ] All packaged slash commands are available and functional after install
- [ ] Team members can complete setup without additional support

## Testing & VQA

### Functional

- [ ] Plugin initializes correctly and exposes the expected interface
- [ ] Workflow lifecycle hooks execute in the correct order
- [ ] Configuration loading works with valid and invalid inputs (error handling)

### Visual / Design QA

- [ ] N/A — this is a non-visual plugin

### Accessibility

- [ ] N/A — this is a non-visual plugin

## References

- [Research: Claude Code Plugin Model](research/claude-code-plugin-model.md)
