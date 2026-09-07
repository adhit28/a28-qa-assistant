# A28 QA Assistant

## Overview

A reusable coding-agent skill for strict, evidence-backed QA and release-readiness checks, with an `agents/openai.yaml` metadata file for Codex. Maintained by adhit28.

## Why Use It

Use this skill before release or deployment when a project needs a disciplined, evidence-backed assessment instead of a list of generic concerns. It prioritizes observed defects and clearly separates confirmed failures, unverified risks, and improvement suggestions, making the resulting report more actionable for release decisions.

## What It Helps With

- Running and interpreting tests, builds, lint, typecheck, and startup checks
- Reviewing app behavior, UI defects, runtime errors, and broken flows
- Checking production readiness, deployment risks, and environment assumptions
- Performing QA-level security checks from concrete repository evidence
- Reporting findings with severity, evidence, impact, reproduction steps, and fix direction

## Use in Codex

Invoke the skill from Codex:

```text
$a28-qa-assistant test this app for broken behavior, layout issues, security risks, and deployment readiness
```

For other LLM runtimes, use the same core `SKILL.md` workflow and check `adapters/` for runtime-specific notes.

For a narrower pass:

```text
$a28-qa-assistant run smoke QA on this feature before release
```

## Requirements and Scope

The skill uses the project’s available tests, runtime, and browser tooling; unavailable checks must be reported as untested rather than passed. It avoids destructive commands, data migrations, load tests, security attack tooling, and audit-fix commands unless the user explicitly approves them.

## AI Model Support

This package declares no model-specific requirement. In Codex, use the model configured for the session, provided it can load skills. Outside Codex, a coding agent may use the Markdown instructions when it can read `SKILL.md` and access the relevant repository, test, and optional browser tools. The skill does not add model capabilities, credentials, or test infrastructure.

## Repository Topics

Suggested GitHub topics:

```text
ai-skill codex-skill claude-skill qa release-readiness testing security-review deployment
```
