# Systemic Action Format

Every remediation item a blameless review produces carries exactly four fields, and an item missing any one of them is not an action.

## The Four Fields

| Field | Question it answers | Rejection rule |
| ----- | ------------------- | -------------- |
| Condition changed | Which of the conditions that produced the failure is now different? | Rejected if it names a person, an agent, or a state of mind |
| Mechanism | What enforces the change — a hook, a schema, a gate, a permission, or a document? | Rejected if the mechanism is intention; "we will remember" is not a mechanism |
| Owner | Which named person or role lands it? | Rejected if the owner is "the team", "everyone", or unassigned |
| Observable | What can be checked later to prove it took effect? | Rejected if it cannot be observed without asking someone whether they felt more careful |

## Mechanism Strength

Prefer the strongest mechanism the condition permits, and say why a weaker one was chosen when it was.

- **Guard or hook** — blocks the action at the moment it is attempted; strongest, and the only class that survives an operator who never reads the doc.
- **Schema or type** — makes the bad state unrepresentable rather than detectable.
- **Gate** — a required check in the commit, review, or deploy path; strong if blocking, near-worthless if advisory.
- **Default or configuration change** — shifts the outcome for everyone who does not deliberately opt out.
- **Documentation or checklist** — weakest; acceptable only for conditions that genuinely require judgement, never as the sole remedy for a mechanically preventable failure.

## Accepted Example

```text
Condition changed: landing a branch no longer accepts a worker's self-report as evidence.
Mechanism: blocking pre-merge required check on the CI workflow for `main`.
Owner: repository maintainer (named role).
Observable: a merge attempt on a branch with a red or missing check is refused by the platform; verified by one deliberate negative-control attempt.
```

## Rejected Example

```text
Action: the agent will be more careful about merging overnight.
```

This is rejected on three counts.
There is no condition — "more careful" describes a disposition, not a state of the system.
There is no mechanism and no owner, so nothing lands and nobody is accountable for it not landing.
There is no observable, so the action can never be closed on evidence and will be closed on assertion.

## Closing an Action

An action closes when its observable has been observed, not when someone reports it done.
Record the observation and the revision it was observed at.
An action whose observable was never checked stays open, and the review that produced it stays open with it.
