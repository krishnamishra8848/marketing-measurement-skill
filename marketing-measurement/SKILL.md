---
name: marketing-measurement
description: Plan, implement, or audit marketing measurement for websites, mobile apps, and CRM outcomes using GTM, GA4, Google Ads, Meta Pixel, CAPI, Meta App Events, Firebase, Clarity, or AdMob. Use for event parameters, consent, attribution, deduplication, conversion goals, audiences, and delivery verification.
---

# Marketing Measurement

Developed by Krishna Mishra.

## Deliver what the user asked for

For an audit, trace the existing journey and identify the first broken or unverified link. For a plan, produce an event registry, route map and validation plan. For implementation, apply authorized changes to the existing stack and validate them through the normal entry point. Discover available source, account connectors or browser access. Continue source-side work when dashboard access is missing, and identify the exact remaining prerequisite.

## Workflow

1. **Find the business outcome and authority.** Trace acquisition, activation, qualification and revenue. Name the authoritative source for each outcome: a first verified registration, confirmed CRM qualification, verified paid order, provider-confirmed delivery, or a genuine SDK ad impression. Choose the smallest set of events that answers the business questions.
2. **Inventory both ends of every link.** Establish the environment, domain or package/bundle, stream/property/Firebase app, GTM container if present, ad account and conversion action, Meta pixel/dataset/app, and Clarity/AdMob project as applicable. Find duplicates from plugins, inline tags, themes, GTM, SDKs, import and backend jobs. Keep working IDs/history and isolate separate apps even when they share one ad account.
3. **Build the event registry.** For each event record the exact trigger, source of truth, consent purpose, fields, destination-specific names, event ID and value/counting policy. Use the [event and parameter matrix](references/event-parameters.md). Prefer provider standard names and in-place edits of human-readable labels. Use project naming conventions. A configurable convention is **Codex | App | Outcome** for editable labels and **codex_** for custom machine names where supported.
4. **Make the consent decision before delivery.** Map the project's actual privacy choices to each purpose and destination. Handle unknown, denied, granted and revoked states. Enforce approved rules in the browser/SDK and again at backend dispatch. Keep secrets server-side and match data in supported provider fields. Never infer advertising consent from login, payment, phone verification, first-party recommendations, global personalization, or a workspace owner's preference.
5. **Choose routes for the actual action.** For website tags, web GTM, server GTM, direct backend delivery and Clarity, read [website measurement](references/web.md). For Firebase, GA4 imports, Meta SDK/app CAPI and AdMob, read [mobile measurement](references/mobile.md). For Google Ads server upload, Meta matching, Business Messaging and CRM outcomes, read [conversion and matching routes](references/conversion-routes.md). Mix only the routes that solve a stated need.
6. **Configure goals and audiences deliberately.** Choose a reliable, eligible primary goal for each authorized campaign objective, and mark diagnostic or proxy actions for observation where appropriate. Explicitly check counting, value, account-default inclusion and campaign-specific settings. Define audiences using meaningful roles, lifecycle stages or recency windows, with exclusions and a justified retention period. Confirm that eligibility and population support the plan. Read [campaign measurement and optimization](references/optimization.md) for launch readiness, goal selection, audience exclusions and reporting.
7. **Verify and hand off.** Use [verification](references/verification.md) for consent tests, replay, provider receipt and attribution. Report what is configured, deployed, dispatched, accepted, processed, deduplicated and attributed using only the states supported by evidence. Record deployment IDs, time window, QA cases, open gaps, next action and rollback. Keep the event dictionary near the implementation.

## Guardrails that affect implementation

- An issued invoice, payment screenshot, redirect or admin button click is insufficient evidence of a paid order. Use the trusted paid state, stable transaction ID, genuine value/currency and original journey. Publish refunds or adjustments only through supported routes.
- HTTPS, server-side routing and hashing still require purpose-appropriate permission. Keep contacts, secrets, payment details and sensitive form values out of general analytics payloads, URLs, dataLayer, session recordings and diagnostic output.
- A retry reuses the original outcome identity and time. Pause on unknown delivery when the provider lacks safe replay or lookup. Never manufacture identifiers, consent, traffic, purchases or provider receipts.
- Respect the user's requested scope for production releases, campaign changes, access, spend and data transmission. Verify current official requirements before implementing or changing a provider-specific route.
