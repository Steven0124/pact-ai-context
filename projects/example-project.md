# Example: Checkout Latency Reduction

> Delete this file once you've added a real project. It exists to show the schema.

- **Status:** active
- **Domain:** [example-domain](../domains/example-domain.md)
- **Last updated:** 2026-06-09
- **Target:** 2026-06-20

## Current state
Moving. Profiling has pinned the p95 checkout latency to a synchronous call to the pricing service inside the request path. Plan is to move it behind a short-lived cache and fall back to the live call on a miss.

## Next steps
- [ ] Add a 30s cache in front of the pricing lookup
- [ ] Load-test the cache-miss fallback path
- [ ] Roll out behind a feature flag at 10%

## Open blockers / decisions
- **Cache invalidation** — decide whether price changes need to bust the cache immediately or eventual consistency is acceptable. Owner: me + pricing team.

## Timeline
- **2026-06-09** — Profiling identified the pricing-service call as the p95 bottleneck.
- **2026-06-08** — Project opened after the latency alert fired.

## Related
- Domain: example-domain
- Worklog entries: 2026-06-09-example-entry
