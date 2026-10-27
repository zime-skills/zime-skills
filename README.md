# Zime GTM Skills for ChatGPT

**Open-source sales skills for ChatGPT, grounded in your real calls, deals and accounts.**

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Skills](https://img.shields.io/badge/skills-11-orange.svg)](#the-skills)
[![Browse the catalogue](https://img.shields.io/badge/browse-zime.ai%2Fgtm--skills-fe7f50.svg)](https://zime.ai/gtm-skills)

This is the ChatGPT edition of Zime's GTM skills. Each skill is a reusable instruction set (`SKILL.md`) for one go-to-market job: prepare for a sales call, write the follow-up, review a deal, brief you on your day, or build a battlecard from what customers actually said.

Every skill runs on the Zime connector, so ChatGPT works from your recorded calls, CRM deals and accounts instead of guessing. Browse the catalogue at **[zime.ai/gtm-skills](https://zime.ai/gtm-skills)**.

## What is a GTM skill?

A skill is a folder with a `SKILL.md` file. The file's `description` says when to use it, and the body says how: which Zime tools to call, how to work out which call or deal you mean, what the answer should look like, and what it must never do (invent a quote, guess a number, send an email on your behalf).

Skills are written for sales reps, sales engineers, BDRs, customer success, marketing and product managers. They read like a good colleague's playbook, not like code.

## The skills

| Skill | What it does | Category |
|---|---|---|
| [account-research](https://zime.ai/gtm-skills/account-research) | Research a prospect company before outreach: ICP fit and likely buyers. For companies not yet in CRM. | Research |
| [actions-commitments](https://zime.ai/gtm-skills/actions-commitments) | Open action items and commitments: who promised what, by when. One call, one deal, or a whole account. | Execution |
| [call-prep](https://zime.ai/gtm-skills/call-prep) | A prep note before an upcoming call: the biggest risk and two or three things to do. | Workflow |
| [competitive-intelligence](https://zime.ai/gtm-skills/competitive-intelligence) | What customers actually say about competitors, with real quotes from real calls. | Intelligence |
| [create-sales-asset](https://zime.ai/gtm-skills/create-sales-asset) | Account review decks, one-pagers, battlecards, case studies and objection talking points from customer evidence only. | Communication |
| [create-sales-to-cs-handover](https://zime.ai/gtm-skills/create-sales-to-cs-handover) | The Sales to Customer Success handover doc for a deal or account: stakeholders, why we won, open objections, commitments. | Workflow |
| [daily-briefing](https://zime.ai/gtm-skills/daily-briefing) | Your day at a glance: today's meetings, what changed on your deals, what needs attention. | Workflow |
| [follow-up](https://zime.ai/gtm-skills/follow-up) | The follow-up email after a call, using only what was said. Always a draft for you to review. | Communication |
| [review-account](https://zime.ai/gtm-skills/review-account) | One account, one deal or the whole pipeline, as a CRM record or a grounded analysis of risk and next steps. | Intelligence |
| [review-call](https://zime.ai/gtm-skills/review-call) | One call at any depth: the record, a structured recap, or the exact words from the transcript. | Intelligence |
| [skill-builder](https://zime.ai/gtm-skills/skill-builder) | Builds a new skill from a plain-language request, using the Zime connector's tools correctly. | Workflow |

## Use in ChatGPT

You need a Zime account.

1. Add the Zime plugin in ChatGPT.
2. Sign in with your Zime account when ChatGPT asks.
3. Run a skill by typing `@` and its name, for example `@call-prep`. In the ChatGPT desktop app you can also type `/call-prep`.

Need help? See [zime.ai/support](https://zime.ai/support).

## Example prompts

- "Prep me for my 3pm with Acme."
- "Recap yesterday's Northwind demo and list what we committed to."
- "Why is the Globex deal at risk?"
- "Draft the follow-up for this morning's call."
- "What are customers saying about our main competitor this quarter?"
- "Build a battlecard against Competitor X from our calls."

## Data and privacy

Every skill calls the Zime connector (`https://mcp.zime.ai/mcp`), which reads your workspace's recorded calls, CRM deals, accounts and contacts, including people's names, email addresses and phone numbers. Zime keeps the questions sent to it and the answers it returns. Each skill also starts by calling the connector's `skill_used` tool, which records the skill's id, version and name with your user and session in Zime's usage log. Nothing else from your conversation is sent with it.

One skill can send data outside Zime:

| Skill | What is sent | Where |
|---|---|---|
| account-research | The prospect company's and people's public names | ChatGPT's web search |

No skill sends email, writes to your CRM, or runs code. Each skill's "What this sends where" section lists exactly what goes where. See the [Zime privacy policy](https://zime.ai/privacy-policy).

## Frequently asked questions

**Do the skills work without Zime?**
No. They are grounded in your recorded calls, CRM deals and accounts through the Zime connector. Without it, ChatGPT has nothing real to work from.

**Can I use these commercially?**
Yes. Everything here is MIT licensed. See [LICENSE](LICENSE).

**Who wrote them?**
Zime's team and Zime customers. Each skill's page on zime.ai/gtm-skills names the author.

**Where do I report a problem with a skill?**
Open an issue in this repository or write to support@zime.ai.

## About Zime

[Zime](https://zime.ai) is a revenue intelligence platform. It records and analyses sales calls, links them to CRM deals and accounts, and gives AI assistants grounded access to that evidence through the Zime connector at `https://mcp.zime.ai/mcp`.

## License

[MIT](LICENSE). Copyright (c) 2026 Inner Fit Research Inc. (Zime).
