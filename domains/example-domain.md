# Example: Checkout Pricing Path

> Delete this file once you've added a real domain note. It exists to show the shape.

The checkout flow calls the pricing service synchronously to compute the final basket total. This note captures how that path works so the AI doesn't have to re-derive it each time.

## How it works
On checkout, the order service calls `GET /pricing/quote` with the basket contents. The response includes line-item prices, applicable promotions, and the total. This call is on the synchronous request path, so its latency directly affects checkout p95.

## Conventions / gotchas
- Prices are cached upstream for 30s; a quote can be up to 30s stale.
- The pricing service returns `409` when a promotion expires mid-request — the caller must re-quote, not retry blindly.

## Decisions & rationale
We kept pricing synchronous (rather than precomputing at basket-add time) because promotions can change between add and checkout, and showing a stale total at the payment step is worse than a slightly slower checkout.

## Related
- Projects: example-project
