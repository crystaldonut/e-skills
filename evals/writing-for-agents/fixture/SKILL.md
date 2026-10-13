---
name: deploy-check
description: Deploy checker. Use when deploying, shipping, releasing, pushing to production, or going live.
---

# Deploy check

You are a careful senior release engineer. Be thorough and write clear output.

1. Understand the change.
2. Run the tests with `npm run test:ci`.
3. Don't skip the migration check. Never ignore a failing migration.
4. Look at the dashboards until you are comfortable.

Remember to run the tests with `npm run test:ci` before anything else.

## Dashboard reference

The latency dashboard has twelve panels. Panel 1 shows p50, panel 2 shows p95, panel 3 shows p99,
panel 4 shows error rate, and the rest are per-region copies of the first four.
