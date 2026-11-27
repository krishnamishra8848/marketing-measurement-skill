# Marketing Measurement Skill

**Developed by Krishna Mishra**

An open-source Agent Skill for planning, implementing and verifying marketing measurement across websites, mobile apps and CRM outcomes. It covers GTM, GA4, Firebase Analytics, Google Ads, Meta Pixel, Conversions API, Meta App Events SDK, Microsoft Clarity and AdMob.

The agent first identifies the setup surface: owned website, mobile app, or Page. It distinguishes an owned landing page from a social Page or hosted form, then maps the actual outcome to the right platform and verifies delivery. The skill guides your agent through existing code and connected tools. Live operations require your own access and authorization.

**Every setup checks all eight:** GTM, GA4, Meta Pixel, Meta CAPI, Google Ads, Google Ads server-side, Microsoft Clarity, and Meta SDK. The skill identifies the applicable route or gives a concrete reason for a platform exception.

Compare [direct Ads tagging, GA4/Firebase imports and server-side routes](marketing-measurement/references/conversion-routes.md#offer-a-google-ads-route-choice) before choosing an Ads setup.

Server-side tracking can run from an existing website backend. A hosted server-side GTM container is optional. At handoff the agent offers to set a weekly or monthly tracking health reminder.

Deep checks cover [GA4 and Google Ads settings](marketing-measurement/references/ga4-settings.md), [deduplication and original IP handling](marketing-measurement/references/dedup-and-request-context.md), and [site-wide remarketing coverage](marketing-measurement/references/web.md#site-wide-remarketing-coverage).

The [signed-in Meta matching guide](marketing-measurement/references/conversion-routes.md#signed-in-user-matching-on-every-eligible-event) also covers eligible verified email, mobile and a stable external_id on each supported signed-in web/app event, guests, logout, account switches and consent withdrawal.

The [business and CRM playbook](marketing-measurement/references/business-playbook.md) connects tracking to campaign objectives, creative and landing pages, lead qualification, mature cohorts and revenue or contribution targets.

The [lead form data guide](marketing-measurement/references/lead-form-data.md) covers visible form fields, consent, hidden attribution context, backend/CRM storage, and Google/Meta click ID mapping.

## Install for Codex or Claude Code

Download the [latest release](https://github.com/krishnamishra8848/marketing-measurement-skill/releases/latest) or clone the source:

```sh
git clone https://github.com/krishnamishra8848/marketing-measurement-skill.git
```

Copy the entire [marketing-measurement](marketing-measurement/) folder, including its references, into one of these directories:

| Agent | For the current project | For all your projects |
| --- | --- | --- |
| Codex | `.agents/skills/` | `~/.agents/skills/` |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |

Start a fresh session. In Codex, select **marketing-measurement** from the skill picker or invoke `$marketing-measurement`. In Claude Code, invoke `/marketing-measurement`. [Codex installation guide](https://developers.openai.com/api/reference/cli) · [Claude Code skills](https://code.claude.com/docs/en/skills)

## Try it

- **Website:** “Audit my checkout. Map GA4, Google Ads and Pixel/CAPI Purchase, trace the authoritative paid event, and give me a verification plan.”
- **Social Page:** “My Facebook Page sends people to WhatsApp. Help me track conversations and qualified leads using the right source.”
- **App:** “Set up measurement for my marketplace. Separate registration, verified-phone lead, buyer and seller audiences, and approved purchases.”
- **CRM:** “Plan qualified-lead feedback from my website and WhatsApp. Show which identifiers each route needs, and test with synthetic data before sending any live events.”
- **Troubleshooting:** “Meta receives PageView but Purchase is missing. Trace consent, order approval, outbox and provider status. Show where the first break occurs.”

Read the [skill](marketing-measurement/SKILL.md), [event and parameter matrix](marketing-measurement/references/event-parameters.md) [campaign measurement guide](marketing-measurement/references/optimization.md), or [verification exercises](marketing-measurement/references/verification.md).

[MIT License](LICENSE)
