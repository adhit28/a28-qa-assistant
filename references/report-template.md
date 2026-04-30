# QA Report Template

Use this shape for strict QA or release-readiness reports. Keep it concise; omit sections that do not apply.

## Status

`Not ready`, `Conditionally ready`, or `Ready from checked scope`.

One sentence explaining the gate decision with the strongest evidence.

## Findings

List confirmed issues first, ordered by severity.

```text
[Severity] Title
Evidence: command, screenshot, console/network error, or file:line.
Impact: user, security, operational, or deployment consequence.
Repro: exact command or steps.
Fix direction: concrete next action.
```

## Risks And Unknowns

List important areas that could not be verified. State what evidence is missing, such as no staging credentials, no production env values, no test account, unavailable browser, missing deployment target, or audit command unavailable.

## Improvements

List suggestions that are not confirmed defects.

```text
[Priority] Title
Evidence: observed code, UI behavior, command result, missing config, or untested area.
Benefit: why this reduces risk or improves quality.
Suggested change: concrete implementation direction.
Release impact: blocks release, accept as risk, or defer.
```

## Checks Run

- Command or manual check: pass/fail and short result.
- Browser flow: viewport, route, pass/fail, evidence path if any.

## Checks Not Run

- Check name: reason it was skipped.

## Release Gate

State the smallest specific condition required to move forward, such as fixing blockers, accepting a documented risk, adding env values, verifying staging auth, or rerunning a failed build.
