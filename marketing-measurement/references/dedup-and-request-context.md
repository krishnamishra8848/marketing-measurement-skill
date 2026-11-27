# Deduplication and original request context

## Match the deduplication scope

| Route | Required check |
| --- | --- |
| Meta Pixel + website CAPI | Use the same exact event name and one event identity for the same action in the same dataset. Pixel uses `eventID`, CAPI uses `event_id`. Generate that identity once and pass it to both. Different actions receive different IDs. Check same-ID pairing and provider evidence over a representative recent window. |
| Meta SDK + app CAPI | Verify the current app-specific mechanism and SDK automatic events. If a safe shared identity cannot be proven, choose one route per event/build and test upgrades. |
| GA4 ecommerce | Supply a unique nonempty, non-PII `transaction_id` per purchase; preserve it for a legitimate refund association. Do not use the same ID across customers or independent transactions. Verify the actual stream/implementation and keep one authoritative sender. A custom `event_id` is not a general GA4 dedup guarantee. |
| Google Ads | Pass the dynamic transaction/order ID required by the selected route. Check browser and eligible server copies against the actual action and documented key. Separate Ads tag actions and Analytics imports can still both report. Keep a single intended bidding action, including through campaign custom goals. `Count = One` means one conversion per ad interaction and does not replace an order ID. |
| Backend retry | Create one work item per destination/outcome using a durable unique key. Commit it with the authoritative state when feasible. Reuse original IDs, time and value across retries. For a timeout with unknown outcome, reconcile receipt or rely on supported idempotency. |

## Capture the original visitor safely

- Capture actual client IP and user agent at the permission-eligible browser request or trusted edge when a destination requires or benefits from them. Derive the client IP using the hosting platform's documented trusted proxy path. Ignore arbitrary forwarded-header values from untrusted peers. Test direct origin restrictions, multiple approved proxies, IPv4, IPv6 and missing values. Never substitute the admin, webhook provider, worker or proxy IP for a customer's IP.
- For Meta website CAPI, send eligible `client_ip_address` and `client_user_agent` un-hashed in provider fields. Genuine `fbp` and `fbc` are also un-hashed. Assess coverage by genuine ad traffic versus organic visits, and keep original browser context with later paid/qualified events. Omit optional missing fields; when a route requires context you lack, record the gap and use a supported fallback only if eligible.
- For GA4 Measurement Protocol, normally reuse eligible client/app context. If genuinely needed and permitted, use documented `user_location` or `ip_override` for geography. Structured location takes precedence. Keep raw IP out of event parameters, custom dimensions, dataLayer and URLs. For a Google Ads upload, send device context only if supported for the specific action and needed; Google Ads click or supported match fields serve a different purpose.
- Retain that context only for the authorized purpose and period, with restricted access. Redact payloads and provider URLs from general logs including API secrets, click IDs, contact hashes and full IPs.

## Spot a duplicate before releasing

Trace one order through source, browser requests, server dispatch and provider report. Filter by exact destination, action and date. Test reload, repeated webhooks, concurrent approval, a temporary retry and browser/server pairs. Confirm one downstream conversion when both copies belong to one outcome, then repeat with a second order and verify it is counted independently. If counts still disagree, inspect alternate plugins, tags, automatic events, native SDKs, API jobs and Ads imports before adding another sender.

[Meta parameters](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/) · [Meta browser/server deduplication](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/) · [GA4 transaction IDs](https://support.google.com/analytics/answer/12313109) · [Google Ads transaction IDs](https://support.google.com/google-ads/answer/6386790) · [GA4 Measurement Protocol reference](https://developers.google.com/analytics/devguides/collection/protocol/ga4/reference)
