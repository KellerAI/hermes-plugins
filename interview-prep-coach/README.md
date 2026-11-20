# Interview Prep Coach

Interview Prep Coach is a plugin for Hermes Agent. It prepares you for a specific interview: it researches the panel from public professional sources, predicts the questions each interviewer is likely to ask, builds STAR answers from your real experience, runs a mock interview with scored feedback, and drafts your application materials and thank-you notes for you to send.

## Install

```bash
hermes plugins install interview-prep-coach --no-enable
hermes plugins enable interview-prep-coach
```

Listed in the [Hermes plugin catalog](https://github.com/NousResearch/hermes-agent/pull/153925). Portable packages stay disabled until you enable them. Once enabled, the skills appear as `interview-prep-coach:<skill>`.

## Skills

| Skill | Use it when |
|---|---|
| `get-started` | You have just enabled Interview Prep Coach, or want to know what it does and how to start. |
| `interviewer-research` | You know who is on the panel and want a cited, public-source profile of each person. |
| `question-predictor` | You want the questions you are most likely to be asked, ranked and tiered. |
| `answer-crafter` | You want STAR answers built from your real experience, with follow-ups and a 60-second version. |
| `mock-interview` | You want to rehearse with an in-character interviewer and get scored feedback. |
| `questions-to-ask` | You want tailored questions to ask each interviewer. |
| `prep-brief` | You want a one-page cheat sheet or a fuller brief the night before. |
| `debrief` | The interview is over and you want the signals listed with their evidence, and a follow-up plan. |
| `application-package` | You want a tailored resume summary, cover letter, recruiter message or 30-60-90 plan. |

## What it does not do

- It never sends, posts, submits or applies for anything, and never contacts an interviewer, recruiter or employer. Every message is a draft you send yourself.
- It never invents experience. Tailoring rewords what is true.
- It researches only the people you will be interviewed by or are applying to, from public professional sources only. It declines to research job candidates or other private people. Its profiles are not intended to be consumer reports, and Interview Prep Coach is not a consumer reporting agency.
- It never looks up, records, scores or comments on race, color, religion, sex (including pregnancy, sexual orientation and gender identity), national origin, age, disability, genetic information, veteran or military status, marital or family status, citizenship or immigration status (beyond lawful work authorization), health, politics, home addresses, personal accounts or any other legally protected characteristic. It does not record graduation years, career-start dates or photos, or infer protected characteristics from names, schools or history.
- It never predicts or role-plays questions about a protected characteristic. If you report being asked one, the debrief flags it as possibly improper (not legal advice).
- It never signs in anywhere; it stops at login walls.
- A debrief lists signals with their evidence; it gives no overall grade and is not a prediction of the employer's decision.
- It is skills only: no tools, no hooks, no MCP servers, no scripts.

## Disclosure

- No network calls of its own, no model calls of its own, no telemetry.
- No scripts, no background processes, no stored credentials, no compiled binaries.
- Uses your agent's own web search to read public pages for interviewer and company research, citing each source with the date read. Sends nothing to KellerAI.
- Your resume and notes are used only in the conversation: web searches contain only the interviewer's name and title, the company and the role, never your name, resume or notes. It does not save your resume, notes or interviewer profiles to persistent memory unless you ask. Outputs are printed as Markdown for you to keep.

## License and credit

Apache-2.0. See `LICENSE` and `NOTICE`.

Built by KellerAI (https://kellerai.io). KellerAI on X: [@KellerAI_KAI](https://x.com/kellerai_kai) · Jonathan Bowe, Co-Founder & COO, on X: [@KellerAI_COO](https://x.com/KellerAI_COO) · LinkedIn: https://www.linkedin.com/in/jonathan-bowe-kellerai

KellerAI is not affiliated with or endorsed by Nous Research, xAI or OpenAI.
