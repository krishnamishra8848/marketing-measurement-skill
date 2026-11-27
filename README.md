# Marketing Measurement Skill

**Developed by Krishna Mishra**

An open-source Agent Skill for planning, implementing and verifying marketing measurement across websites, mobile apps and CRM outcomes. It covers GTM, GA4, Firebase Analytics, Google Ads, Meta Pixel, Conversions API, Meta App Events SDK, Microsoft Clarity and AdMob.

The agent first identifies the setup surface: owned website, mobile app, or Page. It distinguishes an owned landing page from a social Page or hosted form, then maps the actual outcome to the right platform and verifies delivery. The skill guides your agent through existing code and connected tools. Live operations require your own access and authorization.

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
