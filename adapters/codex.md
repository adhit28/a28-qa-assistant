# Codex Adapter

Use the core `SKILL.md` instructions as the source of truth.

- Keep `name: a28-qa-assistant` unchanged so `$a28-qa-assistant` continues to work.
- Keep `agents/openai.yaml`; it is Codex/OpenAI UI metadata.
- Prefer available Codex shell, browser, Playwright, screenshot, MCP, and source-inspection tools for evidence.
- Follow Codex sandbox and approval rules before installing dependencies, running networked checks, or executing risky commands.
- Do not run destructive commands, migrations, load tests, audit-fix commands, or attack tooling without explicit approval.
