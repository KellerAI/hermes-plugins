# Hook Desk

Hook Desk is a plugin for Hermes Agent. It studies the opening lines of posts you paste and builds a sourced formula file you can copy, keep and paste back in later. It names the pattern in each hook, explains why it may work and drafts new opening lines in your voice for you to approve. Every formula links the post it came from. Engagement numbers are recorded only as you supply them, and anything it cannot check is labelled unverified.

## Install

```bash
hermes plugins install hook-desk --no-enable
hermes plugins enable hook-desk
```

Listed in the [Hermes plugin catalog](https://github.com/NousResearch/hermes-agent/pull/153877). Portable packages stay disabled until you enable them. Once enabled, the skills appear as `hook-desk:get-started` and `hook-desk:hook-forensics`.

## Skills

| Skill | Use it when |
|---|---|
| `get-started` | You have just installed Hook Desk. It asks for three sample posts, words or topics to avoid, and the platforms you write for. |
| `hook-forensics` | You paste a post and want to know why its opening worked, want to add it to your formula file, or want opening lines drafted from your formulas. |

## What it does not do

- It does not post, like, reply or browse social platforms. It works only from posts and metrics you paste.
- It makes no promise about reach.
- It is skills only: no tools, no hooks, no MCP servers, no scripts.

## Disclosure

- No network calls, no model calls of its own, no telemetry.
- No shell commands, no background processes, no stored credentials, no compiled binaries.
- Reads nothing outside the text you give it. The formula file lives in the conversation; Hook Desk offers to print it as Markdown for you to keep.

## License and credit

Apache-2.0. See `LICENSE` and `NOTICE`.

Built by KellerAI (https://kellerai.io). KellerAI on X: [@KellerAI_KAI](https://x.com/kellerai_kai) · Jonathan Bowe, Co-Founder & COO, on X: [@KellerAI_COO](https://x.com/KellerAI_COO) · LinkedIn: https://www.linkedin.com/in/jonathan-bowe-kellerai

KellerAI is not affiliated with or endorsed by Nous Research, xAI or OpenAI.
