# elara-agent-prompts

Versioned AI agent prompts and config for [Elara](https://www.lacreadorademundos.com/). n8n workflows fetch these at runtime via GitHub raw URLs, pinned to tagged releases.

## Structure

```
agents/
├── architect/           # World foundation creator
│   ├── prompt.md        # Full prompt for LLM Model
│   └── config.json      # Model, temperature, max_tokens, variables
├── chronicler/          # Daily narrator
│   ├── prompt.md
│   └── config.json
└── (future agents)
```

## How n8n fetches prompts

n8n downloads prompts and config pinned to a specific tagged release:

```
https://raw.githubusercontent.com/lacreadorademundos/elara-agent-prompts/v1.0.0/agents/architect/prompt.md
https://raw.githubusercontent.com/lacreadorademundos/elara-agent-prompts/v1.0.0/agents/architect/config.json
```

To upgrade to a new version, tag a new release (e.g., `v1.1.0`) and update the tag in the n8n workflow.

## Agents

| Agent | Role | Trigger |
|-------|------|---------|
| **Architect** | Creates world foundation (genre, rules, initial state) | Manual (Monday) |
| **Chronicler** | Generates narrative entries per era | Cron (09:00, 14:00, 19:00) |

### Future agents (post-MVP)

- **Memoria** — context compaction for narrative coherence
- **Validator** — quality and coherence checking
- **Illustrator** — descriptive image generation
- **Translator** — multilingual versions

## Config format

```json
{
  "model": "GLM-4.7-Flash",
  "temperature": 0.9,
  "max_tokens": 4096,
  "top_p": 0.95,
  "output_format": "json",
  "variables": ["WORLD_CONTEXT", "CURRENT_ERA"]
}
```

## Versioning

Releases are tagged using semantic versioning (`vMAJOR.MINOR.PATCH`):

- **MAJOR** — prompt rewrite that changes output format or variables
- **MINOR** — prompt improvement (new instructions, tone adjustments)
- **PATCH** — typo fixes, minor wording changes

## Repository license

[CC BY-SA 4.0](LICENSE.txt)
