# Broad QA Checklist

Use this checklist for product behavior and general QA coverage. Use `security-checklist.md` for security depth and `production-readiness.md` for deployment depth. Do not report unchecked items as failures.

## Baseline Commands

- Install or verify dependencies with the repository's package manager.
- Run lint, typecheck, test, and production build scripts when present.
- Start the app locally when UI or runtime behavior matters.
- Capture command failures with the failing command, exit status, and relevant error lines.
- Prefer existing package scripts over invented commands.
- Do not run commands that mutate production data, rewrite dependencies, or apply automatic fixes unless the user asked for fixes.

## UI And Interaction

- Check primary routes at desktop and mobile widths.
- Check core user flows from entry to success state.
- Check form validation, required fields, disabled states, submit behavior, cancellation, and duplicate submission.
- Check loading, empty, error, and permission-denied states when reachable.
- Check links, buttons, menus, tabs, modals, dialogs, drawers, navigation, pagination, filters, and search.
- Check browser console errors, network failures, missing assets, hydration errors, and source-map noise.
- Check keyboard navigation, focus traps, visible focus, labels, accessible names, and obvious contrast failures.

## Layout

- Check text overflow, clipping, overlap, horizontal scroll, unstable dimensions, and broken sticky/fixed positioning.
- Check responsive behavior at mobile, tablet, and desktop sizes.
- Check long names, long words, empty data, many items, and narrow containers.
- Check that important UI is not hidden behind headers, footers, cookie banners, or modals.

## Data And State

- Check create, read, update, delete, optimistic update, refresh, and back/forward behavior when relevant.
- Check state persistence after reload and route changes.
- Check error handling for failed API calls and invalid server responses.
- Check time, currency, number, timezone, and locale handling when present.

## Report Requirements

- Include exact commands run and results.
- Include browser viewport sizes for UI findings.
- Include file and line references for source findings.
- Include screenshot paths when screenshots support the issue.
- Include untested areas explicitly.
- Separate confirmed defects from risks and unverified areas.
- Include prioritized improvement suggestions when evidence shows a concrete way to reduce release, security, UX, reliability, accessibility, performance, or maintenance risk.
