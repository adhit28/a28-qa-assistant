# Security QA Checklist

Use this for evidence-backed security QA. It is not a penetration-test playbook. Do not claim exploitability without a concrete path, affected asset, and supporting code or runtime evidence.

## Triage Rules

- Mark exposed secrets, auth bypass, privilege escalation, unauthenticated sensitive data access, unsafe file upload execution, production debug exposure, and critical dependency advisories as `Blocker` unless proven unreachable.
- Mark missing server-side authorization on sensitive operations, stored or reflected XSS paths, SQL/NoSQL injection paths, insecure direct object references, weak session handling, and high dependency advisories as `High`.
- Mark missing hardening headers, incomplete rate limits, weak validation on low-impact inputs, and unclear security ownership as `Medium` unless paired with a concrete exploit path.
- Mark minor defense-in-depth gaps as `Low`.

## Evidence To Collect

- File and line references for source findings.
- Exact package manager audit command and summary for dependency findings.
- Exact secret pattern or variable name without printing full secret values.
- Request, route, role, or permission boundary for auth findings.
- Browser console or network evidence for client-side issues.
- Configuration file references for headers, CORS, cookies, deploy runtime, and debug flags.

## Secrets And Configuration

- Search for API keys, tokens, private keys, OAuth secrets, database URLs, webhook secrets, service account JSON, cloud credentials, and committed `.env` files.
- Check whether example env files use placeholders rather than real-looking values.
- Check that secrets are loaded from environment or secret manager, not bundled into client code.
- Check that public client environment variables are intentionally public and not server secrets with a public prefix.
- Check logs and error messages do not print credentials, tokens, authorization headers, cookies, or personally identifiable information.

## Authentication

- Identify auth provider, session mechanism, token storage, callback routes, and logout behavior.
- Check that protected routes enforce authentication server-side or at the API boundary, not only with hidden UI.
- Check session cookies use secure settings in production: `HttpOnly`, `Secure`, appropriate `SameSite`, scoped domain/path, and reasonable expiration.
- Check password handling when local passwords exist: hashing with a modern password hashing function, no plaintext storage, no password logging, and safe reset flow.
- Check OAuth callback validation, redirect allowlists, CSRF/state parameter use, and account linking assumptions when OAuth exists.

## Authorization

- Identify roles, ownership checks, tenant boundaries, admin gates, and resource identifiers.
- Check every sensitive read/write/delete/export action enforces authorization on the server.
- Check users cannot change identifiers in URLs or request bodies to access another user's or tenant's data.
- Check admin UI restrictions are backed by server checks.
- Check webhooks and background jobs validate event ownership and source authenticity.

## Input, Output, And Injection

- Check server-side validation for request bodies, query params, route params, file metadata, and webhook payloads.
- Check database access uses parameterized APIs or safe ORM patterns.
- Check dynamic HTML rendering, Markdown rendering, rich text, user-generated content, and `dangerouslySetInnerHTML` paths are sanitized or avoided.
- Check redirects are allowlisted and cannot be used for open redirect attacks.
- Check command execution, template rendering, path construction, and file reads do not use unsanitized user input.

## Browser And API Hardening

- Check CORS is scoped to expected origins for credentialed or sensitive APIs.
- Check CSRF protection for cookie-authenticated state-changing requests.
- Check rate limits, abuse limits, or provider-level protection for login, signup, password reset, OTP, invite, contact, payment, upload, and expensive AI/API routes.
- Check security headers where applicable: `Content-Security-Policy`, `X-Content-Type-Options`, `Referrer-Policy`, `Frame-Options` or CSP frame ancestors, and HSTS for HTTPS deployments.
- Check error responses avoid stack traces, SQL errors, internal IDs that matter, and framework debug pages in production.

## Files, Uploads, And External Integrations

- Check uploads validate size, type, extension, content, storage location, and public access rules.
- Check uploaded files cannot overwrite arbitrary paths or execute as code.
- Check signed URLs, object storage policies, and CDN rules do not expose private files.
- Check webhook signatures, timestamps, replay protection, and idempotency.
- Check payment flows verify server-side status from the provider and do not trust client-side success alone.

## Dependencies And Supply Chain

- Run the repository's audit tool when available: `npm audit`, `pnpm audit`, `yarn npm audit`, `bun audit`, `pip-audit`, `safety`, `cargo audit`, `govulncheck`, or the ecosystem equivalent.
- Record critical/high advisories with package name, severity, affected range, fix availability, and whether the vulnerable path is used.
- Check lockfile presence and package manager consistency.
- Check postinstall scripts, unpinned external scripts, CDN dependencies, and build-time code generation for unexpected risk.

## Reporting Security Findings

- Do not paste full secrets. Show only a redacted prefix/suffix or variable name.
- Separate confirmed vulnerabilities from hardening recommendations.
- State what was not tested, such as no live staging access, no authenticated test account, no production config, or no dependency audit tool.
