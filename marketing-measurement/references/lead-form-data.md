# Lead form fields and acquisition identifiers

Ask what the form is meant to accomplish before choosing fields. A customer supplies contact and qualification information; a tracking integration captures eligible acquisition context. Display only fields a person can answer. Never ask a customer to type an ad click or browser ID.

## Fields the customer sees

| Field | Collect when |
| --- | --- |
| Name or preferred name | The team needs to address or identify the inquiry. |
| Email and phone/mobile | Collect the channel needed for follow-up. Offer both when both have a real purpose; require both only when that purpose warrants it. Track self-reported versus verified status. Use an unambiguous country code for phone normalization. |
| Service/product, short need, preferred contact channel | Useful for routing, qualification or a useful reply. |
| Budget range, timeline, location | Add only when meaningful to service fit. Conditional questions can keep the form short. Keep free text and sensitive answers out of tracking payloads. |
| Privacy notice and choices | Explain the intended use. Record the applicable choice for ads measurement/user-data sharing separately from the customer's request for service. Capture the choice state, purpose, timestamp and notice version as appropriate. |

Never collect credentials, OTPs, payment proof, government identifiers, or unrelated personal details for marketing. Keep first-party contacts and consent evidence in restricted systems. If appropriate, verify contact through the actual product process and record qualification/verification transitions separately.

## Fields captured by the system

| Field | Source and correct route |
| --- | --- |
| `gclid`, `gbraid`, `wbraid` | Actual Google Ads landing URL or a supported integration. Capture when genuinely present and permitted. Choose the exact fields required or supported by the Google Ads/Data Manager action; app/web and legacy routes vary. Retain values as issued. |
| `fbclid`, `_fbc` → `fbc` | Genuine Meta ad click context. Reuse the valid click cookie where permitted, or derive the provider-format `fbc` from a real `fbclid` under Meta's documented rules. No click means no invented `fbc`. |
| `_fbp` → `fbp` | Genuine Meta browser identifier from the authorized web setup. Can be present without an ad click. It is distinct from Google's `gbraid`. Send Meta `fbp` and `fbc` unchanged and unhashed. |
| `ctwa_clid`, native form `lead_id` and form/ad references | Capture from the supported messaging referral or leads integration, not generic URL guessing. Keep the original conversation or provider lead mapping. |
| UTMs, safe landing URL and referrer | Capture a bounded set of campaign parameters and preserve genuine acquisition context across authorized redirects. Strip unrelated query fields, secrets, contacts and fragment content. UTMs supplement click IDs. |
| GA4 `client_id` or Firebase `app_instance_id` | Capture only for an eligible context and when needed for the Analytics route. Preserve a real session reference where applicable. Exclude from user-facing forms and general reports. |
| Original IP and user agent | Collect only where the authorized route needs them, at a trusted edge or request. Never use the approval operator's IP/UA. Follow the [original request context guide](dedup-and-request-context.md). |
| Internal IDs and timestamps | Assign stable opaque lead/event IDs, record form and submit time, consent scope and original acquisition time. Link later genuine qualification or payment to the right opportunity and order. |

For a hosted form that cannot read the original browser context, use the provider's lead/referral integration or a legitimately supported field mapping. Record unavailable IDs as missing. A click token or URL field is neither consent nor authentication.

## Implementation and verification

1. Capture legitimate acquisition context at the eligible landing/request. Preserve the existing Google linker/Meta setup and website consent behavior. Bind permitted context to an opaque first-party journey reference or use provider-supported automatic capture. Avoid copying all cookies or putting user match data in the public dataLayer.
2. On successful form processing, save the lead and link its acquisition context in the backend or CRM. If a hosted form uses hidden fields, allowlist and validate the fields server-side. Do not use hidden fields as proof of identity, permission, or an actual sale.
3. On a genuine stage transition, resolve consent and the original lead/customer. Send only destination-supported IDs and normalized first-party match fields through the intended provider channel. Follow [conversion and matching routes](conversion-routes.md). Use the real event time and stable lead/event/order IDs rather than inventing new conversions on CRM edits.
4. In isolated QA test ad landing, organic landing, a redirect/cross-domain flow, duplicate submit and late qualification. Test missing or forged parameters, denial, revocation and a shared-device account change. Confirm the form still works when tracking context is unavailable, an event only fires on success, and eligible events carry the right IDs with no user PII leakage.

[Google Data Manager event fields](https://developers.google.com/data-manager/api/reference/rest/v1/events/ingest) · [Google enhanced conversions for leads](https://support.google.com/google-ads/answer/11021502) · [Meta fbp and fbc](https://developers.facebook.com/documentation/ads-commerce/conversions-api/parameters/fbp-and-fbc)
