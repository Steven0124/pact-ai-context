# 2026-06-09 — Cached the pricing lookup

> Delete this file once you've logged real work. It exists to show the schema.

- **Type:** feature
- **Tickets/PRs:** EXAMPLE-1, repo#1
- **Project:** example-project

## What
Moved the synchronous pricing-service call on the checkout path behind a 30s in-memory cache, with a live fallback on a miss. Profiling had pinned it as the p95 bottleneck. Early load tests show p95 checkout latency down meaningfully with no correctness regressions on the cache-miss path.

## Artifacts
- PR: https://example.com/repo/pull/1
- Profiling dashboard: https://example.com/dashboard

## Related
- example-project
