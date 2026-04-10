# Plan — WO-002: Create DL-Agent-Workflow Claude Code Plugin

## Approach

Package the DL-Agent-Workflow as a distributable Claude Code plugin by assembling a `plugin/` directory at the repo root. All 10 existing skills and 4 templates are copied into the plugin tree. A `plugin.json` metadata file is authored. Two install scripts (Unix `install.sh` and Windows `install.ps1`) handle copying the plugin into a target repo. `INSTALL.md` and `README.md` document setup and usage. No new workflow logic is needed — this is purely file assembly, scripting, and documentation.

---

## Steps

- [ ] Step 1 — Read all 10 SKILL.md files at `.claude/skills/*/SKILL.md` and verify each has `name`, `description`, `agent: general-purpose`, and `argument-hint` frontmatter; note any issues before copying
- [ ] Step 2 — Create the plugin directory tree: `plugin/.claude-plugin/`, `plugin/skills/` (one subfolder per skill × 10), `plugin/templates/`
- [ ] Step 3 — Write `plugin/.claude-plugin/plugin.json` with fields: `name` (`dl-agent-workflow`), `version` (`1.0.0`), `description`, and `skills` array listing all 10 skill names
- [ ] Step 4 — Copy all 10 `SKILL.md` files from `.claude/skills/{skill}/SKILL.md` into `plugin/skills/{skill}/SKILL.md`
- [ ] Step 5 — Copy 4 templates from `.github/templates/` into `plugin/templates/`; in the `workflow.md` copy replace all project-specific values (`PVT_kwHOD9B30s4BTj7z`, `PVTSSF_lAHOD9B30s4BTj7zzhAyGKQ`, `JBabcock-DL`, all status option IDs) with `[CONFIGURE: ...]` placeholders and inline comments explaining each
- [ ] Step 6 — Write `plugin/install.sh` (bash): validate `gh`, `git`, `bash` on PATH; copy `plugin/skills/` → `.claude/skills/` and `plugin/templates/` → `.github/templates/`; support `--force` flag to overwrite; print post-install checklist
- [ ] Step 7 — Write `plugin/install.ps1` (PowerShell): equivalent logic to `install.sh`; validate prerequisites; copy trees; support `-Force` flag; print post-install checklist
- [ ] Step 8 — Write `plugin/INSTALL.md`: prerequisites (`gh` CLI, `git`, Claude Code); Unix and Windows install commands; post-install steps (replace all `[CONFIGURE]` placeholders in `workflow.md` with real GitHub Project ID, Status field ID, status option IDs, and repo owner)
- [ ] Step 9 — Write `plugin/README.md`: one-paragraph overview; full skills table (all 10 skills, name + one-line description each); link to `INSTALL.md`
- [ ] Step 10 — Smoke-test both install scripts targeting a temp directory; confirm all 10 skill folders and 4 templates are copied; confirm `--force`/`-Force` overwrites without error; confirm `workflow.md` copy contains `[CONFIGURE]` placeholders

---

## Build Agents

<!-- Ordered build phases for the /build orchestrator.
     Agents within a phase run in parallel. Phases run sequentially. -->

### Phase 1 (parallel)
- `code-build` — Steps 1–5: audit skills, scaffold plugin directory tree, write plugin.json, copy all SKILL.md files, copy and generalize templates

### Phase 2 (parallel, after Phase 1)
- `script-build` — Steps 6–7: write install.sh and install.ps1
- `doc-build` — Steps 8–9: write INSTALL.md and README.md

### Phase 3 (after Phase 2)
- `code-build` — Step 10: smoke-test both install scripts against a temp directory

---

## Dependencies & Tools

- **Bash / PowerShell** — writing and testing install scripts (Steps 6, 7, 10)
- **No MCP servers required** — pure file assembly and scripting
- **`gh` CLI** — only for the GitHub board status update after plan approval; not part of the plugin build itself
- **Source files**: `.claude/skills/` (10 skills), `.github/templates/` (4 templates)

---

## Open Questions

1. **`plugin.json` exact schema** — research identified `name`, `version`, `description`, `skills` as likely required fields but the canonical spec is unconfirmed; use best-effort for now and note in README
2. **Install target path** — copy skills directly into `.claude/skills/` (matches current project layout, simple) vs `.claude/plugins/dl-agent-workflow/` (namespaced); direct copy assumed
3. **GitHub Project board scaffolding** — install scripts are file-copy only; board setup is a manual post-install step documented in `INSTALL.md`

---

## Notes

- 10 skills to include: `create-ticket`, `research`, `plan`, `figma-build`, `vqa`, `project-start`, `code-build`, `doc-build`, `script-build`, `api-build` (4 new build skills added after ticket was written — all must be in the plugin)
- `workflow.md` contains hardcoded project-specific IDs that must be generalized before distribution
- Skills namespace as `plugin-name:skill-name` in Claude Code — document this in `INSTALL.md` so users know to invoke `/dl-agent-workflow:create-ticket` or configure aliases
- Build agent for this ticket: use `/script-build` for Steps 6–7, `/doc-build` for Steps 8–9, `/code-build` for Steps 1–5 and 10

---

## Verification

1. Run `bash plugin/install.sh` against a temp dir — confirm 10 skill folders + 4 templates land correctly
2. Run `plugin/install.ps1` on Windows — confirm equivalent output
3. Open a fresh Claude Code session in the temp repo — confirm all 10 slash commands are recognized
4. Confirm installed `workflow.md` has `[CONFIGURE]` placeholders, not real IDs
