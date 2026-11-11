# Reliability Desk

Reliability Desk is a plugin for Hermes Agent. It runs high-reliability practices on your real launches, changes and incidents, borrowed from launch operations, air traffic control, manufacturing, surgery, IT operations and site reliability engineering. Each practice ends in an evidence record: every finding cites the plan, log line or message it rests on, and anything without evidence is marked unverified.

## Install

```bash
hermes plugins install reliability-desk --no-enable
hermes plugins enable reliability-desk
```

Portable packages stay disabled until you enable them. Once enabled, the skills appear as `reliability-desk:<skill>`.

## Skills

| Skill | Use it when |
|---|---|
| `get-started` | You have just enabled Reliability Desk, or want to know what it does and which practice fits. |
| `go-no-go-poll` | You are about to cut or publish a release and want an attributable GO or NO-GO from each discipline. |
| `blameless-incident-review` | An outage, bad agent run or shipped defect is over and you want a review that fixes conditions, not people. |
| `fmea-design-review` | A design or plan needs its failure modes scored and ranked, with owned mitigations. |
| `closed-loop-readback` | An instruction is costly or ambiguous and should be read back and confirmed before anyone acts. |
| `andon-stop-the-line` | You want halt triggers and owners declared before work starts, so a defect stops the line instead of being logged. |
| `change-control-board` | A change has an unclear blast radius and needs a standard, normal or emergency class and a recorded decision before merge. |
| `surgical-safety-checklist` | You are starting risky multi-file or high-stakes work and want sign-in, time-out and sign-out gates. |

## What it does not do

- It does not send, post or page anyone. Escalations and polls are drafts you send yourself.
- It does not merge, deploy, change or delete anything unless you confirm that exact action in the chat.
- It never assigns personal blame, and nothing it writes is meant as grounds for discipline or any other employment action.
- A GO or NO-GO is a recommendation for the named owner, not a decision.
- It is skills only: no tools, no hooks, no MCP servers, no scripts.

## Disclosure

- No network calls, no model calls of its own, no telemetry.
- No scripts, no background processes, no stored credentials, no compiled binaries.
- Works from what you paste or share in the chat. It may suggest read-only inspection (for example `git log` output) with your agent's own tools, and never signs in anywhere.
- Records are printed in the chat as Markdown for you to keep.

## License and credit

Apache-2.0. See `LICENSE` and `NOTICE`.

Built by KellerAI (https://kellerai.io). KellerAI on X: [@KellerAI_KAI](https://x.com/kellerai_kai) · Jonathan Bowe, Co-Founder & COO, on X: [@KellerAI_COO](https://x.com/KellerAI_COO) · LinkedIn: https://www.linkedin.com/in/jonathan-bowe-kellerai

KellerAI is not affiliated with or endorsed by Nous Research, xAI or OpenAI.
