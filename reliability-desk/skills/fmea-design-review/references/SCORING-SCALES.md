# Scoring Scales

Original KellerAI anchors for severity, occurrence, and detection, written for software and agent systems.
They are structured after the general 1-10 convention used in reliability engineering, and no proprietary rating table is reproduced here.
Declare which scale you used in the output before the first number appears.

## Severity (S) — how bad the effect is

Score the worst credible effect of the mode, not the mode's name.

| S | Anchor | Worked example |
| - | ------ | -------------- |
| 10 | Silent corruption or loss of committed data or money, undetectable after the fact | A partial write leaves half a ledger batch applied and nothing records which half |
| 9 | Total loss of the primary function for all users, or a security boundary breached | An auth middleware fails open and every request is treated as authenticated |
| 8 | Total loss of the primary function for a subset of users, recoverable | A tenant's queue consumer crashes and only that tenant stops processing |
| 7 | Primary function degraded enough that users abandon the task | Every request takes 40 seconds under normal load |
| 6 | A secondary function lost entirely | Export-to-CSV returns an empty file while the app otherwise works |
| 5 | Wrong output that the user can notice and correct themselves | A sort order is reversed in a list view |
| 4 | Function correct but requires a manual workaround each time | A retry must be triggered by hand after each deploy |
| 3 | Cosmetic or annoyance-level defect with no functional impact | A timestamp renders in the wrong timezone label |
| 2 | Detectable only by an operator reading logs | A debug warning is emitted on every startup |
| 1 | No perceptible effect on any user or downstream system | An unused config key is ignored |

Occurrence never lowers a severity score.
"It almost never happens" is an occurrence argument.

## Occurrence (O) — how likely the named cause is

Score the likelihood of the specific cause you wrote in the cause column, over a stated window.
State the window: per request, per run, per deploy, or per month.

| O | Anchor | Worked example |
| - | ------ | -------------- |
| 10 | Happens on essentially every occasion | An unbounded retry loop fires whenever the dependency is slow, which is always at peak |
| 9 | Happens most times the code path is exercised | A cache read returns stale data whenever two writers race, and they race hourly |
| 8 | Happens several times a week in normal operation | A flaky integration test fails on roughly one run in three |
| 7 | Happens weekly | A nightly job times out when the input set exceeds the usual size |
| 6 | Happens monthly | A token refresh collides with a deploy window |
| 5 | Has happened a few times and the cause is unchanged | A partial write recurred after two prior incidents |
| 4 | Has happened once, cause understood and partially addressed | A schema drift broke a consumer, and a check was added for that one field |
| 3 | Plausible from the code path but never observed here | A specific ordering of two async writes has not yet been seen |
| 2 | Requires an unusual combination of conditions | A leap-second and a rollover in the same minute |
| 1 | Structurally prevented by the design | The type system makes the wrong call unrepresentable |

If you cannot name a cause, you cannot score occurrence.
Go back and name it.

## Detection (D) — how well today's controls surface it

High is bad.
Score only controls that exist and run right now.
A control you intend to build scores 10 until it is built and observed working.

| D | Anchor | Worked example |
| - | ------ | -------------- |
| 10 | No control exists that could observe this mode at all | A silent truncation with no length assertion anywhere in the pipeline |
| 9 | Detectable only by a user reporting it afterwards | A wrong export noticed by a customer next quarter |
| 8 | Detectable only by a human reading logs on purpose | An error swallowed into a debug line nobody tails |
| 7 | An alert exists but fires after harm has already landed | A data-integrity alarm that runs daily on yesterday's rows |
| 6 | Caught by a manual review step that is sometimes skipped | A checklist item in a runbook |
| 5 | Caught by a test that exercises a mock rather than the real path | A stubbed HTTP client asserts on the stub |
| 4 | Caught by a test that runs only on a nightly schedule | An end-to-end suite outside the pull-request gate |
| 3 | Caught by a test in the pull-request gate | An integration test that fails the build |
| 2 | Caught by a blocking hook or schema rejection before the change lands | A pre-push validation that refuses the write |
| 1 | The mode cannot be expressed, so there is nothing to detect | An illegal state has no constructor |

The gap between D 5 and D 3 is where most agent work over-credits itself.
A passing test that never touched the real path is a mock assertion, and it belongs at 5, not at 3.

## Declaring the scale

Emit one line before the table, for example: scales per `SCORING-SCALES.md`, occurrence window measured per deploy.
Without that line, a later reader cannot tell whether your 7 means their 4, and the table cannot be re-scored by anyone else.
