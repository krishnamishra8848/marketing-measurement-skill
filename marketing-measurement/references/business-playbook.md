# Business-first campaign and CRM playbook

Use after the intake when the user wants a launch strategy, campaign audit, reporting, or sales feedback alongside tracking. An audit can prepare a campaign plan without launching or spending.

## Choose the objective, offer and destination together

| Business situation | First comparison | Useful success signal |
| --- | --- | --- |
| Straightforward offer with a clear price and low-friction checkout | Direct purchase landing page, product page, or in-app checkout | Verified purchase, net revenue, refunds and contribution after acquisition |
| Consultative, high-consideration or custom-price offer | Website lead form, native Instant Form, booked call, or messaging | Qualified opportunity or delivered meeting and eventual sales, not cheap form submits alone |
| Search demand with a small budget | Start with tightly scoped high-intent queries, a relevant landing page and serviceable geography; compare match types and add evidence-based negatives | Relevant search terms, confirmed leads, cost per qualified lead, budget wasted on mismatched intent |
| No reliable conversion signal yet | Separate measurement repair from bidding. Use a bounded diagnostic or traffic test only if useful, with success and stop criteria | Correct attributable signals and observed downstream quality. No universal conversion threshold or requirement to start with traffic. |
| App acquisition and monetization | Compare installs, activation, retention and true ad or purchase revenue from matched cohorts | Cost per retained user and cohort contribution, not downloads alone |

Choose awareness, traffic, engagement, leads or sales in the actual ad platform based on the outcome and destination. A WhatsApp button tap or call click is intent. Use an eligible, confirmed conversation, connected call or qualified outcome when the business goal requires it. Check [call reporting and Google Ads URL options](google-ads-settings.md) for the actual account and region.

For Google Search, group by user intent. Review Search Console for owned organic landing coverage and Business Profile when local listings form part of the journey. Use available Keyword Planner and Search Console evidence together with search-term reports. Tight match types and smaller serviceable areas are options when budget is scarce. Check actual location targeting, networks, destination, and which terms spend money. Pin creative assets only where a required message or experiment justifies it. Consider automated campaign types, broad reach and value bidding after checking the quality and eligibility of the feedback, and read back campaign-specific goals.

## Creative and landing QA

- Define the audience problem, clear offer, proof, one primary CTA and matching destination. Inspect mobile rendering, load path, price/currency, form feedback and checkout. For examples or claims use verified business evidence. Use competitor ad libraries as research input rather than reproducing assets.
- Label creative/landing tests and preserve an intelligible UTM convention. Prefer platform auto-tagging or supported dynamic parameters for acquisition IDs. Preserve final URLs, query strings and redirects through the real destination. Keep contacts and sensitive values out of URL parameters.
- Inspect ad previews across the placements that matter. For a single-video requirement, check catalog, carousel/collection, site links, website extracts, generated artwork and enhancements, then preserve only the requested media. Confirm the effective route after save. Distinguish preparing a draft from publishing it.

## Audiences and experiment design

- Separate acquisition, warm engagement, qualified leads and customers. Use recency windows like 7, 30 or 90 days when the buying cycle and sample support them. Add exclusions for converted customers where appropriate. Check audience thresholds, platform retention and whether targeting values are hard controls or suggestions in the selected campaign.
- Build eligible lookalikes or value-based segments from sufficient genuine customers or qualified outcomes when justified. Document seed definition and exclusions. A live audience entry or eligibility does not establish lift.
- Use a qualified lead or verified conversation for bidding when it is eligible and mature cohorts show it predicts sales. Until then, observe it in a bounded test and set explicit volume, lag and cohort-maturity criteria for revisiting the goal. A/B test the highest-impact variable first and document the decision threshold, stopping rule and measurement horizon. Compare aligned geographies and mature cohorts. A person who entered the funnel yesterday may still buy later. Report cohort windows and sample sizes rather than calling all fresh leads lost.
- Ad-platform attribution can overlap. Use the source ledger for total orders and revenue. Use holdout, geo or other suitable incrementality evidence where practical before attributing a budget increase to a causal lift.

## CRM feedback and the money ledger

1. Model `lead_id`, `opportunity_id` and `order_id` separately. One lead or buyer can produce more than one genuine order. Ingestion time, acquisition time and outcome time can all differ. Log them separately and send the true outcome time.
2. Record form/lead ID, channel, genuine acquisition context and consent before sending feedback. Keep website lead IDs, native form IDs, Messenger page-scoped identifiers and WhatsApp referrals in their supported routes. Read [conversion and matching routes](conversion-routes.md).
3. Qualify with explicit criteria such as need, fit, budget and timeline. Where a form supports it, use conditional questions or branching with minimal friction. Treat unreachable, pending and disqualified as different states. Audit follow-up delay and coverage so the bidding signal does not merely mirror salesperson availability.
4. Reconcile paid invoices, storefront transactions and manually confirmed bank/QR/cash outcomes to the actual order ledger. For manual payment approval, match the amount, currency and unique bank/provider transaction reference against the authoritative payment record, and guard against assigning one payment to multiple orders. Design explicit partial-payment and overpayment handling if the product accepts them. Save gross revenue, fees/refunds, attributable cost and contribution separately. Choose revenue or contribution as the optimization value with the owner, verify destination support and keep the original invoice totals intact.
5. Track eligible outcomes through queued, dispatched, accepted, processed, partial, rejected, expired, missing, corrected and reconciled states where observable. Alert on a growing queue or gaps relative to real eligible outcomes. Use failures and evidence to find the first broken stage.

## Close the loop

Report what you observed, what requires more time/data, and which decision follows. Give a ranked next test or fix, its owner and evidence threshold. Offer the [recurring health check](verification.md#recurring-tracking-health-check) after the setup review. Never label an optimization win solely from more accepted events or a higher match score.

[Google Ads keyword matching](https://support.google.com/google-ads/answer/7478529) · [Google Ads conversion goals](https://support.google.com/google-ads/answer/10995103) · [Google Data Manager upload diagnostics](https://developers.google.com/data-manager/api/devguides/diagnostics) · [Meta lead ads and forms](https://eventsmanager.facebook.com/business/ads/ad-objectives/lead-generation/lead-ads-with-forms)
