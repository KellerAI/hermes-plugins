# Professional Finder

Professional Finder is a plugin for Hermes Agent. It helps a small business, or a person hiring for their own needs, find, shortlist, license-check and vet **licensed or credentialed professionals** in any US state: healthcare, legal, financial, real estate, trades and construction, engineering and architecture, education and more. It works from public professional information only: official license registries, regulator disclosure systems, association directories, and what professionals publish about their own work.

## Install

```bash
hermes plugins install professional-finder --no-enable
hermes plugins enable professional-finder
```

Portable packages stay disabled until you enable them. Once enabled, the skills appear as `professional-finder:<skill>`.

## Skills

| Skill | Use it when |
|---|---|
| `get-started` | You have just enabled it. Four setup questions, then a sourcing plan. |
| `ground-rules` | Loaded first by every other skill: hard rules, FCRA and anti-discrimination cautions, the state licensing-board method, national registries, output conventions. |
| `find-professional` | "I need a [profession] in [place]." Profession category, open questions, tiered sourcing plan, blank shortlist. |
| `prospect-candidate` | "Find me candidates." Search strings, scored longlist, 3-5 person shortlist, **draft** outreach, minimal tracker. |
| `verify-license` | "Is [name] licensed?" A dated verification summary naming the database and URL checked. |
| `screen-candidate` | "Vet this professional before we engage them." A dated credential report from license and regulator records. |

## What it does not do

- It never sends email or messages, posts job ads, books calls, or contacts candidates, employers, references or licensing boards. Outreach is a draft you send yourself.
- It is **not a consumer reporting agency** and does not perform background checks. Its reports summarize public professional-license and regulator records and are not consumer reports under the Fair Credit Reporting Act (FCRA). Do not use them as the basis for an adverse employment action; for a background check, use an FCRA-compliant screening company and talk to employment counsel.
- It screens only on job-related criteria and never on protected characteristics.
- It does not get around CAPTCHAs, login walls or site terms; it looks up one person at a time at a human pace and hands you the exact page when a site blocks automated lookups.

## Disclosure

- Skills only: no tools, hooks, MCP servers, scripts or background processes. No stored credentials, no telemetry, no compiled binaries.
- Uses the agent's own web tools, when you have them enabled, to open public registries and directories. It sends nothing to KellerAI.
- Candidate details stay in your conversation or in a tracker you own. Record only what the hiring task needs and delete records for people you are no longer considering.

## Privacy and terms

KellerAI privacy policy: https://kellerai.io/privacy · Terms: https://kellerai.io/terms

## License and credit

Apache-2.0. See `LICENSE` and `NOTICE`.

Built by KellerAI (https://kellerai.io). KellerAI on X: [@KellerAI_KAI](https://x.com/kellerai_kai) · Jonathan Bowe, Co-Founder & COO, on X: [@KellerAI_COO](https://x.com/KellerAI_COO) · LinkedIn: https://www.linkedin.com/in/jonathan-bowe-kellerai

KellerAI is not affiliated with or endorsed by Nous Research, xAI or OpenAI.
