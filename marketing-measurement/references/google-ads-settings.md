# Google Ads tracking options and call reporting

Audit the effective settings before making any change. Check existing account, campaign and lower-level overrides. Account settings may affect campaigns outside the requested project. Record the current value, intended value, scope and verification.

## URL options and click capture

| Setting | Recommended decision and verification |
| --- | --- |
| Auto-tagging | In Admin → Account settings, verify that Google Ads auto-tagging is **ON** as the default for web conversion measurement. Enable it within the authorized account scope if off, then reopen the setting to verify. Test that the landing page accepts click parameters and that redirects, cross-domain forms and CRM handoffs preserve eligible values. Log any explicit exception and why. |
| Final URL | The exact user-facing destination. Check correct domain, locale, offer, and mobile path. Validate any sitelinks, mobile URLs and dynamic final URLs used by the campaign. |
| Final URL suffix | Use for UTMs and ValueTrack fields that must arrive on the landing page, especially with parallel tracking. An account-level default suits a shared taxonomy; use campaign-specific values or overrides when needed. Enter without a leading question mark. If a destination already has UTMs, resolve conflicts before saving. |
| Tracking template | Add or preserve it when a measurement provider, redirect, or other deliberate routing requires it. For applicable account/campaign/ad group templates, insert the actual final URL with `{lpurl}` or the provider-required escaped variant. Do not copy a third-party redirect example into a live account. If you only need landing-page UTMs, a Final URL suffix can do that without a separate template. |
| Custom parameters and ValueTrack | Use only relevant, supported fields and sensible stable identifiers. Example: `{campaignid}`, `{adgroupid}`, `{creative}`, `{device}`, `{network}`, `{matchtype}` or `{keyword}` where populated. Treat IDs as strings, and handle empty placeholders by campaign type. A Search keyword's ValueTrack value is not proof of the user's exact query. |
| Parallel tracking and overrides | Verify the effective template, suffix and any third-party tracking endpoint. Under parallel tracking, the final landing route and tracker run separately; put parameters required on the landing page in the suffix or actual final URL. Inspect more-specific template and suffix settings before relying on account defaults. |

Example **Final URL suffix** for a straightforward Search campaign. Replace it if the user's campaign naming or channel taxonomy requires different values.

```text
utm_source=google&utm_medium=cpc&utm_id={campaignid}&utm_campaign={campaignid}&utm_content={creative}&utm_term={keyword}
```

Use Google Ads **Test** for URL options, confirm the actual landing URL and redirect chain, then verify a permitted genuine arrival flows into GA4 and persists to the lead record where needed. Correct duplicate query keys and encoding errors. Preserve real click IDs and deduplicated conversion actions. Do not place email, phone, lead PII or credentials in UTMs or tracking URLs. Do not click your own live ads for QA.

[Final URL suffix](https://support.google.com/google-ads/answer/9054021) · [Tracking templates](https://support.google.com/google-ads/answer/6273460) · [ValueTrack](https://support.google.com/google-ads/answer/6305348) · [Auto-tagging](https://support.google.com/google-ads/answer/3095550)

## Calls from ads and call reporting

1. Ask whether phone calls are a real conversion goal. Check account and destination country support for Google forwarding numbers, and the correct call or location asset and business phone. If authorized, eligible and needed, turn **Call reporting ON** under **Admin → Account settings → Call reporting**. Reopen the setting to verify. It can replace the number shown in ads with a forwarding number routed to the business.
2. In **Goals → Conversions → Summary**, inspect the existing **Calls from ads** action before creating another. Review the call source, minimum duration based on actual qualified-call evidence, count, value, window, and whether this action is in account-default or custom campaign goals. If call reporting is enabled, review any automatically included default action. A short accidental tap should not be the primary signal for a qualified-call campaign.
3. Measure separate outcomes deliberately. **Calls from ads** can use eligible call/location assets and forwarding. **Calls from website visits** can use supported website number replacement. A website click-to-call is an intent action. **Calls via uploads** represent eligible calls with a verifiable downstream outcome. Check that one call does not create two bidding signals across click, connected-call and CRM actions.
4. Check call details, duration, connected status and conversion action against authorized business records. If forwarding or call reporting is unavailable, document the gap and use appropriate form, contact-intent or eligible CRM measurement. Call recording/AI qualification has separate availability and privacy requirements. Treat it as its own decision.

[Call reporting settings](https://support.google.com/google-ads/answer/9141717) · [Calls from ads and other call actions](https://support.google.com/google-ads/answer/6095882) · [Forwarding-number availability](https://support.google.com/google-ads/answer/2454052)

## Google Ads measurement settings readback

- Verify correct links to GA4/Firebase, authorized audience exports and personalization, and actual website/app data sources. Verify account/region policy and end-user consent before implementing user-provided data or enhanced conversions.
- For eligible web lead flows, enable the unified Enhanced conversions setting and verify website capture plus CRM upload and diagnostics. Follow the [offline conversions workflow](conversion-routes.md#google-offline-conversions-and-first-party-matching).
- Check the Google tag/destination and conversion-linker behavior, site-wide eligible remarketing, audience diagnostics, cross-domain landing behavior, and native hosted lead-form reporting when applicable.
- Per conversion action, check category, source, count, actual value and currency, click/view windows where supported, attribution model, diagnostics, and account-default and campaign-specific goals. A Primary label alone does not describe every campaign's behavior.
- For supported server delivery, check the destination conversion action, consent, original permitted click/match context, deduplication/adjustments, upload status and actual report. Use the [conversion route guide](conversion-routes.md) for request-level diagnostics.
- Report each finding as verified, pending, unavailable, or not applicable with evidence. Add unresolved items to the [tracking recheck](verification.md#recurring-tracking-health-check).
