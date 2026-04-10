# Research — Claude Code Plugin Model

## Summary

The DL-Agent-Workflow is a mature, well-structured agent workflow system built on GitHub Issues and Claude Code. To package it as a distributable Claude Code plugin, it needs to conform to Claude Code's plugin architecture while preserving existing skills, templates, and conventions.

## Key Findings

### 1. Existing DL-Agent-Workflow Components

The current system includes:
- **6 Functional Skills**: `create-ticket`, `research`, `plan`, `figma-build`, `vqa`, `project-start`
- **4 Templates**: `bug_report.md`, `work_order.md`, `workflow.md`, `agent-handoff.md`
- **Project Context**: `CLAUDE.md` (session context) and `README.md` (user-facing docs)

All skills follow the SKILL.md standard with YAML frontmatter (`name`, `description`, `context`, `agent`, `argument-hint`) and markdown instructions.

### 2. Claude Code Plugin Architecture

Standard plugin directory structure:

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json              # Required metadata
├── skills/                      # Agent Skills (optional)
│   └── skill-name/
│       └── SKILL.md
├── hooks/                       # Event handlers (optional)
├── .mcp.json                    # MCP server integration (optional)
└── README.md                    # Documentation (required)
```

Key insights:
- Plugin metadata goes in `.claude-plugin/plugin.json` (required)
- Skills in plugins automatically namespace as `plugin-name:skill-name` to avoid conflicts
- Plugins work alongside project skills (`.claude/skills/`) without conflicts
- At startup, only skill names and descriptions load; full content loads on invocation

### 3. SKILL.md Conventions

Frontmatter fields in use:
- `name`: skill identifier → becomes `/slash-command`
- `description`: when to use the skill (Claude's decision filter)
- `argument-hint`: expected args for autocomplete
- `context: fork`: runs in isolated subagent
- `agent`: subagent type (`Explore`, `general-purpose`, `Plan`)

String substitution: `$ARGUMENTS` or positional `$0`, `$1` in skill body.

### 4. Installation and Distribution Model

Three distribution scopes:
1. **Project skills**: committed to `.claude/skills/` in a repo
2. **Plugins**: packaged directories with `.claude-plugin/plugin.json` metadata
3. **Managed**: org-wide via managed settings

Install script strategy:
- **Unix**: Copy plugin to `~/.claude/plugins/dl-agent-workflow/` or project `.claude/plugins/`
- **Windows**: PowerShell equivalent

### 5. Configuration and Permissions

The project uses `settings.local.json` to grant tool permissions (Bash/gh CLI, MCP, WebSearch). A distributable plugin should document required permissions in `INSTALL.md`.

## Recommendations

**Proposed plugin directory structure:**
```
dl-agent-workflow/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── create-ticket/SKILL.md
│   ├── research/SKILL.md
│   ├── plan/SKILL.md
│   ├── figma-build/SKILL.md
│   ├── vqa/SKILL.md
│   └── project-start/SKILL.md
├── templates/
│   ├── workflow.md
│   ├── bug_report.md
│   ├── work_order.md
│   └── agent-handoff.md
├── install.sh
├── install.ps1
├── INSTALL.md
└── README.md
```

**Install script should:**
1. Copy plugin to target location
2. Validate `gh` CLI, `git`, and `bash` availability
3. Provide post-install instructions for configuring GitHub Project metadata (Project ID, Status Option IDs)

## Open Questions

1. What is the exact `.claude-plugin/plugin.json` schema and required fields?
2. Should the plugin scaffold a GitHub Project board, or assume users create one manually?
3. Should install scripts validate tool availability or assume a working environment?
4. Should the plugin include version tracking and upgrade paths?
5. Are there naming or licensing conventions for published Claude Code plugins?
