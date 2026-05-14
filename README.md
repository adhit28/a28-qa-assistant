# A28 QA Assistant

A Codex skill for strict, evidence-backed QA and release-readiness checks. Maintained by adhit28.

## What It Helps With

- Running and interpreting tests, builds, lint, typecheck, and startup checks
- Reviewing app behavior, UI defects, runtime errors, and broken flows
- Checking production readiness, deployment risks, and environment assumptions
- Performing QA-level security checks from concrete repository evidence
- Reporting findings with severity, evidence, impact, reproduction steps, and fix direction

## Usage

Invoke the skill from Codex:

```text
$a28-qa-assistant test this app for broken behavior, layout issues, security risks, and deployment readiness
```

For a narrower pass:

```text
$a28-qa-assistant run smoke QA on this feature before release
```

## Safety

The skill avoids destructive commands, data migrations, load tests, security attack tooling, and audit-fix commands unless the user explicitly approves them.

## Repository Topics

Suggested GitHub topics:

```text
codex-skill qa release-readiness testing security-review deployment
```
