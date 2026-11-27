# Event and parameter matrix

Use this as a selection guide. Verify enabled products, current event requirements, applicable consent, and exact platform schemas. These are logical contracts, not one payload to broadcast everywhere.

| Business action | Canonical example | Useful event fields | Qualification |
| --- | --- | --- | --- |
| Landing or page view | `page_view` / Meta `PageView` | Sanitized location, referrer, route, campaign context, event ID if paired | One per intended view. Exclude secret-bearing URL parts. |
| List, select, item view | `view_item_list`, `select_item`, `view_item` / `ViewContent` | Item ID/name, category, list ID, position, item price and currency when meaningful | Match Meta `content_ids` to exact catalog feed IDs. Translate from internal and GA4 IDs if needed. |
| CTA, WhatsApp, call | `contact_click` | Contact channel, placement, public destination label | Intent only. Use provider-specific call reporting when an actual call is the goal. |
| Form success | `generate_lead` / `Lead` | Opaque lead ID, form ID, lead type and time | Success confirmed by server/CRM. Deduplicate repeated submits. |
| Lead qualified | `qualify_lead` or a supported destination event | Stable lead ID, change time, stage, optional documented valuation | Qualification criteria such as verified need and sales intent. A click or auto-response is insufficient. |
| Registration and login | `sign_up` / `CompleteRegistration`, separate `login` | Authentication method, eligible pseudonymous account ID, bounded account role | New-account creation and repeat sign-in are distinct. |
| Phone verified or account ready | `phone_verified`, `account_ready` | Role, lifecycle milestone, verification method if useful | Count once per intended milestone. Map to Lead only if verified signup meets the product's lead definition. |
| Video or filter engagement | `video_engagement`, `filter_apply` or supported recommended events | Content ID, bounded watch milestone, filter group, screen | Keep useful intent signals. Avoid every tap, arbitrary strings and sensitive filter values. |
| Cart and checkout | `add_to_cart`, `begin_checkout` / `AddToCart`, `InitiateCheckout` | Items, quantities, value, currency and stable IDs where applicable | Distinguish checkout initiation from payment. |
| Paid order | `purchase` / `Purchase` | `transaction_id`, `value`, `currency`, `items`; tax/shipping when supported; product IDs aligned to destination | Use verified payment and explicit valuation rules. GA4 item value and separate tax/shipping follow its schema; Ads may optimize for gross order value, net revenue or fees by deliberate choice. |
| Refund | `refund` / supported conversion adjustment | Original transaction ID, real refund items/amount, adjustment identity and time | Model partial and repeated refunds safely. Provider refund support differs. |
| Actual monetized ad impression | SDK `ad_impression` / paid callback where applicable | Ad platform/source, unit/format, paid value and currency | Use one monetary source per platform. Ad request, loaded, shown and paid callbacks have distinct meanings. |

## Assign parameters to the correct lane

| Lane | Examples | Handling |
| --- | --- | --- |
| Event envelope | Event name, source, original event time, opaque event ID, version, environment | Stable across safe retries. Keep ingestion time separately. |
| Analytics | Item ID, screen, source platform, account role, device/app version, checkout step | Allowlist values, avoid high-cardinality dimensions, and register reporting dimensions only where needed. Exclude direct identifiers and raw financial inputs. |
| Journey | Real UTMs, `gclid`/`gbraid`/`wbraid`, `fbp`/`fbc`, applicable `ctwa_clid`, eligible GA4 client or app-instance ID | Capture only permitted IDs in the appropriate first-party store. Preserve original eligible attribution on the lead/order. Distinguish original and subsequent touch. Exclude private IDs from analytics dimensions and public logs. |
| Provider identity | Email, phone, name, city, country, postcode, external ID, original request context where supported | Send only eligible fields using the selected provider's normalization and hashing rules. Omit missing/untrusted values. See [route matching](conversion-routes.md). |
| Revenue | Currency, amount, units, gross/net/fee basis, item/discount/tax treatment | Reconcile to authoritative records. Store minor units where practical and convert to provider units at the boundary. |

## Copyable registry row

| Business event | Exact trigger and source | Purpose | Parameters and ID | Destination and count/value | Verification |
| --- | --- | --- | --- | --- | --- |
| Verified paid order | Payment transitions to verified paid in server ledger | Analytics and eligible ads, evaluated separately | Order ID, original event ID/time, currency, amount, permitted journey reference | GA4 purchase once; Meta Purchase browser/server pair if applicable; selected Ads action once per order | Duplicate callback, reload and approval replay use same outcome; compare ledger, request and report |

This matrix intentionally avoids attaching customer data to general event parameters. For each route verify the platform's supported user-provided data channel and policy before implementation. [GA4 recommended events](https://developers.google.com/analytics/devguides/collection/ga4/reference/events) · [Meta CAPI parameters](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/)
