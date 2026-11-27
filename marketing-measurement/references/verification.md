# Verification and troubleshooting

## Record an evidence chain

| Stage | Evidence to record |
| --- | --- |
| Configured | Exact environment and destination, version, intended goal and identity mapping |
| Deployed | Published GTM version, server release or installed app build as appropriate |
| Dispatched | Sanitized browser network record or outbox state with one stable event ID |
| Accepted | Provider response and documented partial errors or rejects. An HTTP success alone can be insufficient. |
| Processed | Correct stream/property, dataset or conversion action shows the event in the relevant report |
| Deduplicated | Browser/server pairing by same event name and ID, plus supported provider evidence where available |
| Attributed | Actual campaign report credits the real outcome within the applicable model/window |

Run synthetic cases with DebugView, isolated properties and test events as appropriate. For Ads use provider validation or isolated destinations when supported. Keep production out of synthetic success metrics. Use separately authorized real-outcome observation to prove real reports, matching or attribution. Never click your own production ads as a QA step.

## Walkthrough cases

### A. Web checkout succeeds after admin review

- Before approval, payment receipt upload and page refresh do not create Purchase. Approval of a verified paid transaction creates one authoritative outcome.
- Test consent grant, deny, revocation between enqueue and send and original consent missing. Inspect where a saved grant binds to the checkout and order. Record the first stage that fails. Require the correct buyer and original journey context.
- Submit the same verified outcome twice in an isolated environment. Confirm one stable transaction/event ID. If the browser and CAPI both emit, validate their name/ID pair and platform deduplication. Compare totals and currencies to the ledger.
- For a row stuck between send and receipt, classify the failure. Retry transient errors according to policy using the same identity. Repair validation or permission errors first. Unknown send outcome requires lookup or a safely idempotent route before replay.

### B. Marketplace buyer and seller attribution

- Provision a buyer and a seller in staging. Validate new-account registration, repeat login, verified-phone milestone, account switch and return visits. Ensure each receiving destination gets the correct role and only permitted identity.
- Validate GA4 registration/lead events and intended Google Ads imports, role-audience membership rules and actual Meta app transport. Confirm SDK/CAPI upgrades do not emit both copies unexpectedly.
- Compare one genuine monetized impression's currency and value against the source. An app button press or failed ad load should never create monetary revenue.

### C. WhatsApp and CRM

- Distinguish an ad click, referral-bearing conversation, verified qualified lead and paid outcome. Test genuine and absent click identifiers and already-qualified retries.
- Show that a saved CRM draft cannot appear as sent or accepted until the provider returns evidence. Route to Business Messaging or a supported offline channel only when the event's actual source matches.

### D. Great match score, missing business outcome

- Check whether the displayed metric describes a different event, date, source or dataset. Inspect coverage by eligible cohort, dedup, order linking and account grant evidence.
- Validate amount, currency, count, selected goals and report windows before adjusting any bidding. Use same-period comparable cohorts. An accepted request or a high score cannot prove incremental sales.

## Handoff checklist

- List changed routes and their business purpose, known IDs and editable goals.
- Include test environment/time, sample identities as opaque references, outcomes and provider screens checked.
- Record open verification gaps, access blockers, consent limits and rollback location. Keep secrets and customer rows outside shared artifacts.
- Scope any remediation to the first evidenced failure and test adjacent paths before claiming resolution.

## Recurring tracking health check

At handoff, state which checks passed, which are pending, and when they were last verified. Then ask: **“Should I remind you to recheck tracking every 7 days, once a month, or not at all?”** If cadence was already specified, use it. Confirm a start or local time only when needed. Use the agent's supported reminder or automation tool when available. Confirm creation and show the next run when the scheduler provides it. If scheduling is unavailable, provide a short copyable calendar reminder with the checklist. Only report an active reminder after the scheduler confirms it.

The reminder should point to the saved event/route inventory and ask the owner to check:

- Recent genuine provider deliveries against the source ledger or CRM, with the intended Ads action, stream, dataset and date window.
- Missing or duplicate Purchase and Lead, currency and value, campaign goal selection and recent attribution or consent changes.
- Browser and mobile behaviour after deployments or SDK updates, including consent and revocation, callback overlap and recording masking.
- Last successful send, oldest pending job, errors and last verified provider receipt. Confirm next action and owner for any gap.

Use read-only evidence unless more is authorized. A reminder to recheck and an automated live audit are separate tasks. A quiet period without orders is insufficient to establish a fault. Never fire synthetic production conversions or alter campaign settings as part of the reminder.
