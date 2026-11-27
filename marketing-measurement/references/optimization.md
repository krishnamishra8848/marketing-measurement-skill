# Campaign measurement and optimization

Use this for launch-readiness reviews, audience design, campaign goal selection, and decisions about where to spend next. Campaign changes and spending need scope separate from measurement validation.

## Before spending

1. State the business decision and define its denominator. Examples: paid orders per attributed click, qualified leads per landing session, purchase value per ad spend, or 30-day net ad revenue per installed cohort.
2. Trace the real destination and intended conversion source. Validate redirects, deep links, campaign UTMs, auto-tagging, website versus WhatsApp destination, and creative enhancements. Inspect the intended source/dataset and all applicable placements, including generated variants. Compare landing view, contact intent, received message, qualification and paid order as distinct stages.
3. Choose a primary conversion goal based on the actual decision. For sales, use a reliable measured sale when eligible. For lead generation, favor a verified meaningful outcome. If value data is sparse, assess a valid proxy against downstream success. Document why secondary actions are diagnostic and confirm account-default and campaign-specific goal scopes.
4. Check current provider eligibility, volume, conversion lag and data quality before changing bidding. A small sample, a universal conversion threshold, or a platform recommendation alone cannot establish the right bidding mode. Record a baseline and define when to revisit it.

## Audience and retention design

- Use bounded, useful segments such as buyers, sellers, qualified leads, purchasers and recent engaged users. Define include/exclude rules, source and consent eligibility, and choose a justified lookback. Compare recent windows with longer windows only where the buying cycle and audience size support it. Longest available membership is an option when purpose and retention permit it.
- Check actual audience population and eligibility in each destination. Plan suppression of converted users when acquisition is the goal, and keep relevant upsell audiences separate when authorized.
- Use a documented attribution model and window for comparisons. Ad-platform credit, backend sales, and incremental lift answer different questions. For budget decisions, prefer comparable cohorts and an incrementality experiment where practical.

## Reporting and operations

Use a bounded dashboard with date, platform, source, event and delivery-state filters. Show aggregate volumes, last accepted event, oldest pending job and error categories by route. Use opaque references for investigation and keep raw payloads and identity away from general reporting access. Alert on broken delivery, stale refresh or a growing retry queue using evidence tied to the actual business outcome.

Compare same-region, same-period data for app monetization. Report impressions, yield, revenue, retention and sample size. Compare acquisition cost with cohort revenue over matched windows and account for fees/refunds; avoid inferring profitability from a handful of impressions or an all-country average.

Record what each metric represents so the team can distinguish a calling or WhatsApp tap from a received conversation, a qualified lead from a contact, and a real payment from an optimization value assigned to a lead.
