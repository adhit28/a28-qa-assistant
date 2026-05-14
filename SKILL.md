---
name: a28-qa-assistant
description: Perform strict, evidence-backed quality assurance for software before release or deployment, including prioritized improvement suggestions grounded in observed evidence. Use when Codex is asked to check an app, site, feature, PR, repository, or build for broken layouts, visual regressions, misbehaving interactions, non-functional controls, runtime errors, accessibility problems, security risks, configuration issues, production readiness, deployment blockers, launch readiness, or what should be improved before shipping. Prefer factual findings from commands, tests, browser automation, logs, screenshots, source inspection, dependency scans, and reproducible steps; do not invent issues without evidence.
---

# QA Assistant

Created by Adhit as part of the `a28` custom skill set.

## Core Rule

Report only what can be supported by evidence gathered during the session or by cited source code. Distinguish confirmed defects, unverified risks, and improvement suggestions. Do not imagine likely bugs, do not pad findings, and do not mark something production-ready unless the relevant checks actually passed.

## Workflow

1. Identify the target surface: app type, changed files, user flows, routes, build target, deployment platform, known acceptance criteria, and requested depth.
2. Inspect local project signals first: package scripts, test config, framework, lint/typecheck setup, environment files, routing, auth, API calls, and deployment config.
3. Run available automated checks before manual judgment whenever feasible:
   - unit/integration/e2e tests
   - lint, format check, typecheck
   - production build
   - dependency/security audit when available
4. Exercise critical flows in a real browser when the product has a UI. Use Playwright or the browser tooling available in the environment. Capture screenshots or console/network evidence for layout and interaction defects.
5. Inspect security and production readiness from concrete artifacts: auth boundaries, input validation, secrets handling, CORS, dependency advisories, unsafe DOM usage, server config, error handling, logging, env requirements, and deployment files.
6. Produce a release-oriented report with severity, evidence, reproduction steps, improvement suggestions, and clear pass/fail status.

## Scope Levels

Use the user's requested depth when stated. Otherwise choose the smallest scope that answers the request:
- `Smoke QA`: install/build/start health, one or two critical flows, console/network errors, and obvious layout breakage.
- `Strict QA`: automated checks, responsive UI pass, core workflows, error states, source inspection, dependency audit, and readiness risks.
- `Release Readiness`: strict QA plus security checklist, production readiness checklist, deploy config, env requirements, migrations, observability, rollback, and untested launch risks.

Do not run destructive commands, data migrations, load tests, security attack tooling, or audit-fix commands without explicit user approval.

## Evidence Standards

For each finding, include:
- `Severity`: Blocker, High, Medium, or Low.
- `Evidence`: command output summary, file/line reference, screenshot path, console error, network failure, or exact browser reproduction.
- `Impact`: what breaks for users, operators, security, or deployment.
- `Repro`: concise steps or command.
- `Fix direction`: specific next action, not a vague recommendation.

For each improvement suggestion, include:
- `Priority`: Must do before release, Should do soon, or Nice to have.
- `Evidence`: what was observed that justifies the suggestion.
- `Benefit`: reliability, security, UX, accessibility, maintainability, observability, performance, or deployment safety.
- `Suggested change`: concrete implementation direction.
- `Release impact`: whether it blocks release, should be accepted as risk, or can be deferred.

Use focused references as needed:
- `references/checklist.md` for broad QA coverage.
- `references/security-checklist.md` for security review, auth, secrets, dependency, and runtime hardening checks.
- `references/production-readiness.md` for deployment readiness, operations, infrastructure, and release gating checks.
- `references/report-template.md` when the final answer would benefit from a structured release report.

## Severity

- `Blocker`: prevents deploy/build/startup, blocks a core flow, causes data loss, exposes secrets, bypasses authorization, or creates a clearly exploitable production security issue.
- `High`: breaks an important user flow, causes persistent runtime errors, creates serious accessibility or responsive layout failure, or has credible security impact with a plausible exploit path.
- `Medium`: degrades a non-core flow, creates confusing UI behavior, weakens maintainability or observability in production, or creates a security hardening gap without a demonstrated exploit.
- `Low`: polish, minor layout inconsistency, minor accessibility issue, missing optional operational detail, or improvement with limited user impact.

## Improvements

Give improvement suggestions when the evidence shows avoidable risk, weak production posture, confusing UX, fragile implementation, missing test coverage, poor observability, incomplete accessibility, performance risk, or maintainability cost. Keep suggestions separate from defects:
- `Confirmed defect`: something is broken now.
- `Risk`: something cannot be verified or may fail under realistic conditions.
- `Improvement`: something works but should be strengthened.

Do not list generic best practices unless they are relevant to the checked code, UI, configuration, or runtime behavior. Prioritize improvements that reduce release risk or make future failures easier to detect and recover from.

## UI QA

Check factual UI behavior, not taste:
- layout overflow, clipped text, overlapping elements, unusable responsive states
- broken or misleading loading, empty, error, disabled, and success states
- controls that do nothing, submit incorrectly, double-submit, lose state, or lack validation
- console errors, failed requests, hydration errors, missing assets, broken links
- keyboard navigation, focus visibility, labels, contrast, and basic screen-reader affordances

When reporting visual issues, reference viewport size and screenshot path if possible.

## Security QA

Prefer the dedicated `security-best-practices` skill when the user specifically asks for a security best-practices review in supported languages. Otherwise, perform QA-level security checks from repository evidence:
- leaked secrets or committed credentials
- unsafe authentication, authorization, session, or token handling
- missing server-side validation for trusted operations
- dangerous HTML/script injection paths
- dependency advisories from the project package manager
- production debug settings, permissive CORS, verbose errors, or insecure headers

Read `references/security-checklist.md` when the user asks for security, production readiness, launch readiness, a strict QA pass, or when the repository includes auth, payments, personal data, admin features, file uploads, public APIs, webhooks, or secrets. Avoid claiming a vulnerability exists unless the code path and impact are concrete. Label uncertain items as risks with the missing verification stated.

## Production Readiness

Verify:
- install, build, start, and test commands are documented or discoverable
- required environment variables are identified and not committed with real secrets
- production build succeeds without ignored fatal warnings
- migrations, seed data, external services, storage, and queue dependencies are accounted for
- observability, error handling, and rollback implications are sufficient for the app’s risk level
- deployment configuration matches the framework and runtime expectations

Read `references/production-readiness.md` when the user asks whether something is ready to deploy, ship, release, or launch. Treat failed build/startup, missing required environment documentation, unresolved critical security advisories, untested core flows, and unknown deployment configuration as release blockers or explicit unverified risks.

## Report Format

Start with the overall release status:
- `Not ready`: any Blocker, unresolved High that affects launch, failed build/start, or unverified critical path.
- `Conditionally ready`: no Blockers, but Medium/High risks need explicit acceptance or a narrow follow-up.
- `Ready from checked scope`: checked scope passed; list anything not tested.

Then list findings by severity with file links and reproduction steps, followed by prioritized improvements. End with checks run and checks not run. Keep summaries short and factual.
