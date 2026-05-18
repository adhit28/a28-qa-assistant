# Claude Adapter

Use the core `SKILL.md` instructions as the source of truth.

- Treat `agents/openai.yaml` as Codex/OpenAI-only metadata.
- Use Claude's available project, artifact, connector, browser, MCP, terminal, or tool-use capabilities when configured.
- Do not assume shell, browser, screenshot, network, repository, or dependency-audit access unless the Claude environment exposes those tools.
- If automated checks cannot be run, mark them as not tested and separate confirmed defects from unverified risks.
- Preserve the release-readiness standard: status, findings by severity, improvements, checks run, and checks not run.
