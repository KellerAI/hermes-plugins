# KellerAI plugins for Hermes Agent

One plugin per folder. Each folder is a portable Agent Plugins v1 package (`plugin.json` + `skills/`) that Hermes Agent installs and loads.

| Folder | Plugin | What it does |
|---|---|---|
| [`hook-desk/`](hook-desk) | Hook Desk | Studies the opening lines of posts you paste, keeps a sourced formula file and drafts opening lines for your approval. Never posts. |
| [`professional-finder/`](professional-finder) | Professional Finder | Finds, shortlists, license-checks and vets licensed professionals in any US state from public records. Drafts outreach; never contacts anyone. Not a background check. |
| [`reliability-desk/`](reliability-desk) | Reliability Desk | Runs go/no-go polls, blameless incident reviews, FMEA, readbacks, stop-the-line triggers, change control and session checklists on your real work, with cited evidence. Never sends or changes anything itself. |
| [`interview-prep-coach/`](interview-prep-coach) | Interview Prep Coach | Researches the panel from public professional sources, predicts questions, builds STAR answers from your real experience, runs mock interviews and drafts application materials you send yourself. |

All are skills only: no tools, hooks, MCP servers, scripts, stored credentials or telemetry. See each folder's README for install steps and disclosure.

## License and credit

Apache-2.0 (see `LICENSE`, `NOTICE` and each folder's `NOTICE`).

Built by KellerAI (https://kellerai.io). KellerAI on X: [@KellerAI_KAI](https://x.com/kellerai_kai) · Jonathan Bowe, Co-Founder & COO, on X: [@KellerAI_COO](https://x.com/KellerAI_COO) · LinkedIn: https://www.linkedin.com/in/jonathan-bowe-kellerai

KellerAI is not affiliated with or endorsed by Nous Research, xAI or OpenAI.
