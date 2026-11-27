---
name: marketing-measurement
description: Plan, implement, or audit marketing measurement for websites, mobile apps, social Pages, hosted forms, and CRM outcomes using GTM, GA4, Google Ads, Meta Pixel, CAPI, Meta App Events, Firebase, Clarity, or AdMob. Use for event parameters, consent, attribution, deduplication, conversion goals, audiences, and delivery verification.
---

# Marketing Measurement

Developed by Krishna Mishra.

## First ask where the action happens

For a new setup, begin with: **“Where do you want tracking set up: an owned website, an Android/iOS app, or a Page?”** If they say Page, ask whether it is a landing page they control, a Facebook/Instagram Page, or a hosted form. Ask where the intended outcome actually completes, such as a website checkout, in-app purchase, platform form, or WhatsApp conversation. If the user already gave clear answers, restate the chosen route briefly and proceed. For mixed journeys, map each step before choosing tools and assign each conversion its actual source.

| Surface or outcome | Start here |
| --- | --- |
| Owned website or owned landing page | Verify the domain and use [website measurement](references/web.md). Scoped landing pages can use the existing site tags with route-specific triggers. |
| Android or iOS app | Verify the package or bundle and use [mobile measurement](references/mobile.md). Start with the app stream, native SDK and eligible Ads imports. |
| Facebook/Instagram Page, hosted form or messaging | Use [Page and hosted conversion measurement](references/pages-and-hosted-conversions.md). Choose native insights, lead-form reporting, campaign destination, messaging or CRM feedback based on the actual action. |

## Required platform coverage

Every setup plan, audit, and handoff must include all eight rows below. For each, report the applicable route, existing or proposed configuration, verification evidence, and a next action. Use **Configured and verified**, **Configured, verification pending**, **Needs setup**, **Blocked**, or **Not applicable**, with a concrete reason. Implement applicable routes within the user's authorized scope. A full audit includes every row even when the destination's architecture requires only some of them.

| Required check | Owned website or landing page | Native mobile app | Social Page or hosted conversion |
| --- | --- | --- | --- |
| GTM | Inspect the web container or plan an appropriate web tag architecture. Check server GTM separately if warranted. | Check app-specific GTM only when supported and warranted by the existing Firebase architecture. | Check owned destinations for web tags. Hosted surfaces use native controls. |
| GA4 | Check property, web stream, events and key events. | Check the Firebase Analytics app stream, consent and events. | Check any connected website or app funnels. Use native Page or form reporting for on-platform actions. |
| Meta Pixel | Check the correct pixel/dataset, browser events and consent. | Check any owned web surface involved. Native activity uses app events. | Check a linked owned website if applicable. Use native reporting for on-platform activity. |
| Meta CAPI | Check eligible website backend events and Pixel deduplication. | Check the app CAPI route and SDK overlap. | Check the actual messaging, lead-feedback, or offline source where the workflow supports it. |
| Google Ads | Check account, correct goal and chosen website tag or GA4 import. | Check Firebase/GA4 link and intended app conversion imports. | Check an eligible native Google lead form or the actual Google Ads destination. Record scope if only Meta activity exists. |
| Google Ads server-side | Check support for server GTM, Data Manager or an eligible direct/backend route. Identify the exact supported conversion type. | Check eligible backend routes separately from Firebase/GA4 imports. | Check eligible CRM feedback or Google-hosted form outcomes. Avoid cross-platform assumptions. |
| Microsoft Clarity | Check project, consent and masking on owned pages. | Evaluate the supported mobile SDK for the app's platform and privacy needs. | Check owned destinations. Use native platform insights on hosted surfaces. |
| Meta SDK | Check any native app connected to the journey. Website measurement uses Pixel/CAPI. | Check the Meta App Events SDK, app identity, consent, and its relationship to CAPI. | Check a connected native app when there is one. |

For native apps include **Firebase Analytics** explicitly under GA4. Include **AdMob and impression revenue** when the app monetizes through ads. A Google Ads import does not satisfy the server-side row. A Meta Pixel or CAPI installation does not satisfy the native SDK row. A stack choice is only complete when every row has evidence or an explicit rationale.

## Deliver what the user asked for

For an audit, trace the existing journey and identify the first broken or unverified link. For a plan, produce an event registry, route map and validation plan. For implementation, apply authorized changes to the existing stack and validate them through the normal entry point. Discover available source, account connectors or browser access. Continue source-side work when dashboard access is missing, and identify the exact remaining prerequisite.

## Workflow

1. **Find the business outcome and authority.** Trace acquisition, activation, qualification and revenue. Name the authoritative source for each outcome: a first verified registration, confirmed CRM qualification, verified paid order, provider-confirmed delivery, or a genuine SDK ad impression. Choose the smallest set of events that answers the business questions.
2. **Inventory both ends of every link.** Establish the environment, domain or package/bundle, stream/property/Firebase app, GTM container if present, ad account and conversion action, Meta pixel/dataset/app, and Clarity/AdMob project as applicable. Find duplicates from plugins, inline tags, themes, GTM, SDKs, import and backend jobs. Keep working IDs/history and isolate separate apps even when they share one ad account.
3. **Build the event registry.** For each event record the exact trigger, source of truth, consent purpose, fields, destination-specific names, event ID and value/counting policy. Use the [event and parameter matrix](references/event-parameters.md). Prefer provider standard names and in-place edits of human-readable labels. Use project naming conventions. A configurable convention is **Codex | App | Outcome** for editable labels and **codex_** for custom machine names where supported.
4. **Make the consent decision before delivery.** Map the project's actual privacy choices to each purpose and destination. Handle unknown, denied, granted and revoked states. Enforce approved rules in the browser/SDK and again at backend dispatch. Keep secrets server-side and match data in supported provider fields. Never infer advertising consent from login, payment, phone verification, first-party recommendations, global personalization, or a workspace owner's preference.
5. **Choose routes for the actual action.** For website tags, web GTM, server GTM, direct backend delivery and Clarity, read [website measurement](references/web.md). For Firebase, GA4 imports, Meta SDK/app CAPI and AdMob, read [mobile measurement](references/mobile.md). For Google Ads server upload, Meta matching, Business Messaging and CRM outcomes, read [conversion and matching routes](references/conversion-routes.md). Offer eligible direct Ads tagging, GA4/Firebase import and server-side options with reporting latency and recommendation. Mix only the routes that solve a stated need.
6. **Configure goals and audiences deliberately.** Choose a reliable, eligible primary goal for each authorized campaign objective, and mark diagnostic or proxy actions for observation where appropriate. Explicitly check counting, value, account-default inclusion and campaign-specific settings. Define audiences using meaningful roles, lifecycle stages or recency windows, with exclusions and a justified retention period. Confirm that eligibility and population support the plan. Read [campaign measurement and optimization](references/optimization.md) for launch readiness, goal selection, audience exclusions and reporting.
7. **Verify and hand off.** Use [verification](references/verification.md) for consent tests, replay, provider receipt and attribution. Report what is configured, deployed, dispatched, accepted, processed, deduplicated and attributed using only the states supported by evidence. Record deployment IDs, time window, QA cases, open gaps, next action and rollback. Keep the event dictionary near the implementation.

## Guardrails that affect implementation

- An issued invoice, payment screenshot, redirect or admin button click is insufficient evidence of a paid order. Use the trusted paid state, stable transaction ID, genuine value/currency and original journey. Publish refunds or adjustments only through supported routes.
- HTTPS, server-side routing and hashing still require purpose-appropriate permission. Keep contacts, secrets, payment details and sensitive form values out of general analytics payloads, URLs, dataLayer, session recordings and diagnostic output.
- A retry reuses the original outcome identity and time. Pause on unknown delivery when the provider lacks safe replay or lookup. Never manufacture identifiers, consent, traffic, purchases or provider receipts.
- Respect the user's requested scope for production releases, campaign changes, access, spend and data transmission. Verify current official requirements before implementing or changing a provider-specific route.
