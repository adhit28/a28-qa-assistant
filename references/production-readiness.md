# Production Readiness Checklist

Use this when judging whether an app, site, service, feature, or PR is ready to deploy. Treat readiness as a gate based on checked evidence, not optimism.

## Release Status Rules

- Use `Not ready` when build/start fails, the app cannot run, a core flow is broken, a Blocker security issue exists, required environment variables are unknown, deployment config is missing for the intended platform, or critical checks were impossible to run.
- Use `Conditionally ready` when no blocker is confirmed but there are unresolved High/Medium risks that need owner acceptance, staging verification, migration planning, or operational follow-up.
- Use `Ready from checked scope` only when build/start/tests for the requested scope pass, core flows were checked, required deployment settings are known, and untested areas are explicitly listed.

## Build And Runtime

- Verify clean dependency install or explain why existing install was reused.
- Run production build, not only development server startup.
- Run production start or preview command when available.
- Check runtime version requirements: Node, Python, Go, Java, Docker base image, package manager, and lockfile.
- Check build output for ignored fatal warnings, missing assets, route generation errors, hydration errors, and environment access failures.
- Check static assets, public paths, image optimization, routing rewrites, API routes, and serverless/runtime compatibility.

## Configuration And Environment

- Identify required environment variables from code, config, schema, docs, and deployment files.
- Check example env files exist and use safe placeholders.
- Check production-only settings are represented: public URL, API base URL, auth callback URL, cookie domain, database URL, storage bucket, webhook secrets, payment keys, email provider, analytics, and feature flags.
- Check development defaults cannot silently ship to production.
- Check config validation fails fast when required variables are missing.

## Data And Migrations

- Identify database, ORM, migrations, seed data, and generated client requirements.
- Check migrations are committed, ordered, and have an intended deployment step.
- Check destructive migrations, backfills, and schema changes have rollback or mitigation notes when relevant.
- Check indexes, constraints, uniqueness, and pagination for user-facing queries likely to grow.
- Check backups, restore expectations, and data retention when the app handles important user data.

## External Services

- Identify third-party APIs, auth providers, payment providers, email/SMS services, object storage, queues, search, analytics, AI providers, and maps.
- Check required credentials and webhook endpoints are documented or discoverable.
- Check failure behavior for external outages, rate limits, timeouts, retries, and partial failures.
- Check webhooks are idempotent and can tolerate retries.
- Check paid or quota-limited services have usage controls when the app can trigger cost.

## Observability And Operations

- Check error boundaries or equivalent user-facing failure handling.
- Check server logs include useful context without leaking secrets or personal data.
- Check monitoring, alerting, health checks, uptime checks, or platform-level equivalents for the app's risk level.
- Check source maps, stack traces, and debug output are configured intentionally for production.
- Check admin/support workflows for diagnosing failed jobs, failed payments, failed emails, and stuck user states when relevant.

## Performance And Reliability

- Check obvious large bundle warnings, unbounded client rendering, expensive server queries, N+1 patterns, missing pagination, and blocking startup work.
- Check caching strategy for static assets and expensive data.
- Check timeout handling, retry limits, abort behavior, and graceful error handling.
- Check mobile and slow-network behavior for primary UI flows when the product is frontend-heavy.

## Deployment Platform

- Check deployment files for the intended platform: Dockerfile, compose files, Vercel/Netlify config, Railway/Fly/Render config, Kubernetes manifests, CI workflows, or platform docs.
- Check build command, output directory, install command, start command, health check path, region/runtime, and routing rewrites.
- Check serverless limitations: file system writes, long-running jobs, streaming, cron jobs, WebSockets, and background work.
- Check secrets are expected to be configured in the deployment platform, not committed.

## CI And Release Process

- Check CI runs lint, typecheck, tests, and build for deployable branches.
- Check failing checks cannot be bypassed accidentally where branch protection is expected.
- Check release notes, versioning, migration order, feature flags, rollback path, and smoke-test plan for risky changes.
- Check there is a minimal post-deploy verification list for core routes and flows.

## Final Report Requirements

- List commands run with pass/fail.
- List critical flows manually checked with viewport/device details when UI is involved.
- List deployment assumptions and missing production inputs.
- List blockers first, then accepted risks, then follow-up improvements.
- Never state "production ready" without naming the checked scope.
