# Conversion routes and matching

## Google Ads

| Need | Route | What to verify |
| --- | --- | --- |
| Optimize for suitable GA4 or Firebase events | Link property and import eligible events | Correct source stream, Ads action and campaign goal, one intended conversion per outcome, reporting delay and attribution |
| Improve matching for allowed website form or purchase signals | Google tag or GTM with enhanced conversions for web | Eligible first-party user-provided data mapped via the supported field, consent and diagnostics. Check supported server-side options for the particular action. |
| Deliver trusted CRM and offline outcomes or eligible additional server-side events | Google Data Manager API or supported Data Manager integration | Correct Ads customer/action and ingestion source, schema, consent, click ID and eligible first-party match fields, transaction ID, time zone and status |
| Centralize tagging infrastructure | Server-side GTM where justified | Container, requests/clients, downstream tags, consent forwarding, transport/retries and end-to-end behavior |

For new Google offline conversion and enhanced-conversions-for-leads integrations, follow the current migration and Data Manager documentation. Legacy Google Ads API paths have eligibility restrictions. Record the exact endpoint and action type instead of treating all server-side Google tracking as one system.

Check auto-tagging and that each eligible lead carries the original genuine click ID where available. Use provider-supported matching fields and actual conversion dates/amounts. Record upload/retrieval status separately from attributed reporting and observe the applicable time window. Keep transaction identity and value stable across permitted retries. For dual imports and tags, distinguish duplicate delivery, duplicate bidding and duplicate totals in reporting. Secondary actions can still appear in All conversions and can be used for bidding when included in a campaign custom goal. Segment by conversion action, inspect account-default and custom goals, and verify one outcome in the intended bidding path. Disable the obsolete sender or import only after a verified cutover, preserving useful history. [Primary and Secondary actions](https://support.google.com/google-ads/answer/10995103)

## Offer a Google Ads route choice

After identifying the surface and objective, show the eligible route options and recommend one. If the user already chose an eligible route, confirm that choice and continue.

| Option | Best fit | Google Ads reporting freshness |
| --- | --- | --- |
| Direct Google Ads conversion tag, deployed through web GTM or a Google tag | Owned website with a reliable browser conversion signal and a need for quicker Ads reporting | Google's comparison lists about **3 hours for last-click** and **15 hours for other models**. GTM can dispatch at the event trigger. Dispatch time does not tell you when the report or bidding will use the conversion. |
| GA4 key event or Firebase event imported into Google Ads | Existing Analytics event contract, especially eligible native app conversions, or a funnel where a shared event definition matters | Google's comparison lists **12 hours for last-click** and **24 hours for other models**. The import guide says data can take up to **24 hours** to appear in Ads. GA4's own reports can take **24–48 hours** to process and stabilize. These describe different stages. |
| Eligible server-side Google Ads route | Server-verified orders, CRM-qualified leads, or a deliberate supported server-side tag implementation | Check the chosen Google Ads or Data Manager route, provider processing, validation and attribution. Web-tag and GA4-import timings do not establish a server upload schedule. |

Offer direct website Ads tracking for quicker reporting when it fits, and keep GA4 available for analytics if requested. Offer Firebase/GA4 import for supported app events. Confirm **one intended bidding action** per business outcome per campaign and check any custom goals. If there is a reason to run both for comparison, keep the observation action out of bidding goals and report by action. A planning estimate such as **1–2 hours** can be recorded as a measured project observation when evidence supports it. Avoid promising that timeframe or a fixed Smart Bidding processing time.

[Google Ads data freshness comparison](https://support.google.com/google-ads/answer/2544985) · [Google Ads GA4 import timing](https://support.google.com/google-ads/answer/2375435) · [GA4 reporting freshness](https://support.google.com/analytics/answer/11198161)

## Meta by conversion source

- **Website:** Link the correct website pixel/dataset. For a simultaneous browser and server copy, share the exact event name and event identity. Browser Pixel uses `eventID`; CAPI uses `event_id`. For a server-only confirmed outcome, prefer one authoritative sender unless a legitimate buyer-side copy is designed and validated.
- **Native app:** Verify the app/dataset and use the app-specific SDK/CAPI schema and policy. Do not copy website identifiers into app events just because a form has similarly named fields.
- **Business Messaging:** Use the actual linked messaging account/channel and supported conversion events. Bind the original referral `ctwa_clid` to its conversation when eligible. For a qualified lead sent after a verified CRM transition, check the current schema for `action_source=business_messaging`, `messaging_channel=whatsapp`, the linked business messaging account/dataset, event fields and supported event name, such as `QualifiedLead` where eligible. If the click ID is absent, check current fallback requirements and omit the event if no supported eligible match path exists.
- **Offline/CRM:** Choose the real source of the action, such as phone or in-store, and the supported API. Under authorized setup, check dataset-to-ad-account tracking assignment and available auto-tracking settings. A CRM sending events does not change their original source. Keep separate identities for different outcomes and one Purchase per sale.

## Website CAPI matching rules

| Field | What to send when permitted and supported |
| --- | --- |
| `em`, `ph` | Actual eligible customer email and phone, normalized and SHA-256 hashed according to Meta’s exact rules. Use verified contact where the project requires it. |
| `fn`, `ln`, `ct`, `st`, `zp`, `country` | Permitted, reliable values normalized and hashed as documented. Omit unavailable or unnecessary fields. Review automatic website matching separately from automatic event generation. |
| `external_id` | Stable approved first-party identity per provider guidance. Scope identity to the right account and environment. |
| `fbp`, `fbc` | Genuine browser/click-derived values, un-hashed. Use a valid captured click to construct `fbc` only per Meta's documented method. Leave absent for visits without an eligible click or cookie. |
| `client_ip_address`, `client_user_agent` | Original user request values where allowed and applicable, un-hashed. Apply a trusted proxy configuration, and never substitute approval operator, worker or hosting IP/UA. Check required field behavior before sending events without original context. |
| Event context | `event_name`, genuine `event_time`, `event_id`, true `action_source`, sanitized `event_source_url` where applicable, and supported `custom_data` such as item IDs and value/currency. |

Check missing fields by eligible source cohort. Organic traffic often has no eligible click ID. Match quality can improve with more accurate fields on eligible events; score improvements and increased attribution require evidence. Hashing and automatic matching do not establish permission. Review consent at event generation and dispatch, preserve stable job identifiers, never backfill activity from a denied period solely because a later grant exists, and do not send a duplicate Purchase to fill reporting gaps.

[Google Data Manager events](https://developers.google.com/data-manager/api/devguides/events) · [Google enhanced conversions for web](https://support.google.com/google-ads/answer/13258081) · [Google enhanced conversions for leads](https://support.google.com/google-ads/answer/11021502) · [Meta CAPI parameters](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/) · [Meta deduplication](https://developers.facebook.com/docs/marketing-api/conversions-api/deduplicate-pixel-and-server-events/) · [Meta Business Messaging](https://developers.facebook.com/docs/marketing-api/conversions-api/business-messaging/)
