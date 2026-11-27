# Website measurement

## Choose an architecture

- Use existing web GTM when it already governs browser tags and consent. If the site owns routing in source and only needs a few integrations, direct browser tagging and a backend sender can be simpler.
- Choose server-side GTM when a managed first-party tagging endpoint, shared transformations or provider routing justify infrastructure, monitoring and maintenance. Confirm client parsing, trusted proxy boundaries, DNS/TLS, consent forwarding and downstream tags. A server container does not itself confirm a native app, Pixel, CAPI or Ads integration.
- Direct backend API delivery fits trusted outcomes such as paid orders and qualified leads. Use an existing queue or an idempotent outbox. GA4 Measurement Protocol supplements browser/SDK collection. Keep separate route owners so tags and backend jobs do not duplicate a conversion.

### Direct from your own website server

A WordPress plugin, Next.js backend, existing API or worker can send events directly over HTTPS to provider endpoints. **You can keep web GTM for browser tags and use your own backend for server delivery without buying or provisioning server-side GTM.**

| Destination | Direct route |
| --- | --- |
| Meta | Send eligible web events from your backend through Meta CAPI. Pair with Pixel using the same event name and ID when both legitimately emit the same outcome. |
| GA4 | Use Measurement Protocol for eligible server events alongside the normal browser or Firebase collection. Use the right stream and eligible client identity. |
| Google Ads | Use a supported Data Manager or other eligible direct route for the chosen Ads action and event source. Check current account and action eligibility and confirm one bidding action per outcome. |

Example: The payment webhook or verified order transition writes the original order event and one job per eligible provider. The worker checks consent, supplies the correct destination and genuine matching context, then stores sanitised receipt and retry state. The browser can continue measuring product views and checkout intent. Preserve the same event identity through retries.

Compare expected hosting and maintenance costs, credentials, queue/retry support, and diagnostics. Recommend server-side GTM if centralised tagging or a supported tag integration solves a requirement the direct backend route cannot cover well. If the current backend already covers the requirements, reuse it.

[Meta Conversions API](https://business-auth.facebook.com/business/tools/conversions-api) · [Google Data Manager events](https://developers.google.com/data-manager/api/devguides/events)

## Implement in order

1. Inspect GTM published version and workspace, code, CMS integrations and plugins. Find each Google tag, Meta Pixel, Clarity script and server sender. Export or record the rollback version and snapshot the route matrix. Verify existing Google Ads auto-tagging, cross-domain journeys and real acquisition parameters where relevant. Preserve genuine query IDs through approved redirects without forwarding unrelated private parameters.
2. Decide what loads under each purpose. If using Google Consent Mode, set purpose-specific defaults before tags and apply CMP updates across page loads and SPA changes. Review basic versus advanced behavior with the project owner. Denied-mode behavior may still send restricted signals in an advanced setup. Make the intentional choice and validate the network against it. Forward the actual decision to applicable server routes. Configure Meta and Clarity consent controls for their own products.
3. Build a single browser event producer per journey. Use a versioned dataLayer contract with bounded values. For commerce include item arrays and map canonical item identity to provider identifiers. For SPAs decide who owns route views and avoid duplicating initial views or Enhanced Measurement. Preview decisions in Tag Assistant before publishing.
4. Configure GA4 property/stream, recommended events and required key events. Assign the trusted Purchase owner. For a backend Measurement Protocol route, use the eligible web client identity and applicable session context, credential storage and current policy. Validate through the debug endpoint and verify live ingestion independently. Keep raw PII out of event params and URLs.
5. Configure Google Ads actions. Use the selected direct tag/eligible server route or a GA4 import according to the [conversion routes](conversion-routes.md), with a clear bidding owner for each business outcome. Verify titles, IDs, category, counting, currency/value, account-default inclusion and campaign-specific goals.
6. Configure Meta Pixel by choosing event mappings, applicable advanced matching and the deduplicated CAPI companion where appropriate. Inventory automatic events and plugins for extra PageView or Purchase emitters. Validate access and exact dataset before enabling a server sender.
7. Configure Clarity for UX investigation. Verify correct project ID, supported consent signal, sensitive-input masking and network behavior before recording. Mask checkout, login, payment proof, account and private CRM areas. Block recording where adequate masking cannot be demonstrated. Keep analytics identity and sensitive contact data out of recording labels. Use recordings to explain friction and provider reporting to prove conversions.

Test both ad landing and clean organic journeys, and check consent on first load, reload, SPA navigation, cross-domain checkout and revocation. For landing-page ads verify the actual final URL and intended placement; audit automatic creative additions if the user specifies a single asset.

[Google Tag Manager server-side](https://developers.google.com/tag-platform/tag-manager/server-side) · [Google Consent Mode](https://developers.google.com/tag-platform/security/guides/consent) · [GA4 Measurement Protocol](https://developers.google.com/analytics/devguides/collection/protocol/ga4) · [Clarity consent](https://learn.microsoft.com/en-us/clarity/setup-and-installation/consent-mode) · [Clarity masking](https://learn.microsoft.com/en-us/clarity/setup-and-installation/clarity-masking)
