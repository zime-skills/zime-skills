# Contributing to Zime GTM Skills for ChatGPT

Thanks for helping make ChatGPT better at go-to-market work. This guide explains where these skills come from, what a good skill looks like, and what to do when you find a problem.

## Where these skills come from

Skills are written and published in the Zime dashboard. The versions here are adapted for ChatGPT by the Zime team, so please don't send a pull request that edits `skills/`. Open an issue instead and we'll make the change.

Pull requests are welcome for everything else: this guide and the README.

## How to contribute a skill

1. Sign in to the [Zime dashboard](https://app.zime.ai), open **Skills**, and choose **New skill**.
2. Write it. The **skill-builder** skill can draft one from a plain-language request and knows the Zime connector's tools.
3. Set the visibility to **Open source** and publish.

Your skill is scanned and listed on [zime.ai/gtm-skills](https://zime.ai/gtm-skills) with your name, role, company and, if you add it, your LinkedIn profile. Publishing open source always credits the author.

## How to improve an existing skill

Only a skill's author can edit it. If you see a way to make one better:

- Open an issue here titled with the skill's slug, for example `follow-up: handle calls with no next step`. Describe what went wrong and what you expected.
- Or publish your own variant under a different name. Say in the description how it differs.

## What a good skill looks like

**The description is the trigger.** ChatGPT reads it to decide when to use the skill, so write it as the requests a person would actually make: "Use for 'prep me for my 3pm', 'what should I know before the Acme call'". Say what the skill does not cover. Keep it under 1,024 characters.

**The body is the playbook.** In this order:

1. What the skill produces and for whom.
2. How to work out what the user means (which call, which deal) and what to do when it is ambiguous.
3. Which Zime tools to call and in what order.
4. The shape of the answer, in plain markdown.
5. Guardrails: use only real evidence from calls and CRM, never invent quotes or numbers, never send anything on the user's behalf, say plainly when something is unknown.

**Naming and metadata**

- Slug: `kebab-case`, a verb or the thing it produces (`call-prep`, `follow-up`, `review-account`).
- Category: one of `workflow`, `research`, `communication`, `intelligence`, `execution`.
- Roles: pick the roles it serves (AE, SE, BDR, Marketing, PM, CS).
- Reference files live in `references/`, `assets/` or `scripts/` only.

**Tone.** Write for a sales rep, not a developer. Short sentences, plain words, no jargon the reader would not use themselves.

## Content rules

Every publish runs a content scan. A skill is held, not published, if it contains:

- Links outside `zime.ai` and its subdomains. Most other hosts are blocked.
- Anything that looks like a credential, token or API key.
- Instructions that try to override the assistant's own guidance or another skill.
- Hidden characters such as zero-width spaces.

Skills here also must not:

- Tell the assistant to use a different connector. A skill uses the Zime connector's tools.
- Rely on features of one assistant, such as placeholders like `$ARGUMENTS` or special output blocks.
- Include customer names, deal values or call excerpts from real accounts. The skill should fetch those at run time through the connector.

## Testing before you publish

Run the skill in ChatGPT against a real call or deal you have access to. Check that:

- It triggers on the phrasings in its description and not on unrelated ones.
- Every fact in the answer traces back to a call or CRM record.
- It says "unknown" rather than guessing when the evidence is not there.

## Reporting problems

- **A skill gives wrong or made-up output:** open an issue with the skill slug, the prompt you used, and what came back. Redact customer details.
- **Install or connector problems:** see [zime.ai/support](https://zime.ai/support) or email support@zime.ai.
- **Security concerns:** email support@zime.ai with "security" in the subject rather than opening a public issue.

## Code of conduct

Be respectful and specific. No harassment, no spam, no sharing of confidential customer information. Maintainers may close issues or decline contributions that do not meet this bar.

## License

By publishing a skill as open source you agree that it is released under the [MIT License](LICENSE), the same license as everything else here. You keep the credit; everyone gets to use it.
