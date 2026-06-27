# AGENTS.md

## Project Overview

Versioned AI agent prompts and config for Elara. This repo contains **only prompts and configuration** — no executable code.

n8n workflows fetch these at runtime via GitHub raw URLs pinned to tagged releases.

---

## Repository Structure

```
/
├── agents/
│   ├── architect/
│   │   ├── prompt.md       # Prompt for LLM model
│   │   └── config.json     # Model params (temperature, max_tokens, variables)
│   └── chronicler/
│       ├── prompt.md
│       └── config.json
├── .gitignore
├── README.md
├── AGENTS.md
└── LICENSE.txt
```

---

## How to Evolve This Repo

### When modifying a prompt

1. Keep prompts in **US English** (both instructions and generated content)
2. Verify that `{{VARIABLES}}` in `prompt.md` match the `variables` array in `config.json`
3. Ensure the JSON output format is consistent with what n8n expects to parse
4. Test the prompt manually before committing if possible

### When adding a new agent

1. Create `agents/<agent-name>/` with `prompt.md` and `config.json`
2. Use English kebab-case for the directory name
3. Update `README.md` agents table
4. Tag a new release following SemVer

### When updating model params

Only change model, temperature, max_tokens or top_p in `config.json`. These are read by n8n at runtime — no code changes needed in workflows.

---

## Critical Rules

### No commit or push without explicit authorization

| Action | Allowed? |
|--------|----------|
| Read files | Yes |
| Create/modify files | Yes |
| `git status`, `git diff`, `git log` | Yes (read-only) |
| `git add` / `git commit` / `git push` | Only with explicit user authorization |

---

## Technical Notes

- Prompts and generated content are in **US English**
- Config is in **English**
- n8n fetches prompts via GitHub raw URLs pinned to tags (e.g., `v1.0.0`)
- Output format: JSON with `world`/`foundation` (architect) or `entry`/`entities`/`context_update` (chronicler)
- Models: GLM-4.7-Flash (architect), GLM-4.5-Flash (chronicler)

---

## Versioning

Releases are tagged using semantic versioning (`vMAJOR.MINOR.PATCH`):

- **MAJOR** — prompt rewrite that changes output format or variables
- **MINOR** — prompt improvement (new instructions, tone adjustments)
- **PATCH** — typo fixes, minor wording changes

---

## Commit Style

- **Language:** US English
- **Format:** `<type>: <description>`

| Type | Use |
|------|-----|
| `feat:` | New agent or prompt |
| `fix:` | Prompt correction or fix |
| `chore:` | Config update, maintenance |
| `docs:` | Documentation changes |

**Examples:**
```
feat: add translator agent prompt
fix: update chronicler variables in config
chore: adjust architect temperature to 0.9
```
