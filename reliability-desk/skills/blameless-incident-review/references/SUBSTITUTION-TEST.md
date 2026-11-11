# Substitution Test

The single question that decides whether a finding is about a person or about the conditions they worked in.

## The Question

> Would another competent operator, holding the same information, the same tooling, and the same time pressure, plausibly have acted the same way?

"Operator" here is whichever entity took the action under review: a subagent, an orchestrator, a human reviewer, or a CI job.
"Same information" means the prompt, the acceptance criteria, the files actually read, and the transcript state at the moment of the action — not what could have been discovered with unlimited time.
"Same tooling" means the tool surface, the guard and hook configuration, and the permissions that were live at the time.

## The Three Answers

| Answer | What it means | What the finding becomes |
| ------ | ------------- | ------------------------ |
| Yes | The conditions steered any competent operator toward the same action | A condition finding: change the prompt, the gate, the guard, or the criteria |
| No | The action departed from what the same conditions would produce | Record the departure as a condition question: why did the system allow it to go undetected? Never classify intent or culpability; that is outside this review |
| Unknown | The evidence does not settle it | Name the missing evidence and treat the gap itself as a detection finding |

A "no" answer is not a licence to name a culprit.
It narrows the question to why the system permitted a departure to reach production undetected, which is again a condition.

## Worked Example — Test Passes

An orchestrator merged a feature branch to `main` at 02:10 and CI went red overnight.
Its acceptance criteria said "land the branch when the worker reports done"; no pre-merge CI gate existed on the branch, and the worker's report was the only available signal.
Substituting any competent orchestrator with that criterion, that signal, and no gate yields the same merge.
The test passes, so the finding is: the acceptance criterion accepted a self-report as landing evidence, and no mechanism required a green check.

## Worked Example — Test Fails

A reviewer approved a change after the guard denied its push, then re-ran the push with a hand-written approval token.
The denial message stated the reason and the guard's behaviour was documented.
A competent reviewer with the same denial and the same documentation would have stopped and reported.
The test fails — and the review still asks the condition question: why was a hand-written token accepted at all, and what mechanism now makes that path impossible rather than merely discouraged?

## Condition-Shaped Wording

Rewrite every actor-shaped finding before it enters the record.

| Actor phrasing | Condition phrasing |
| -------------- | ------------------ |
| The agent was careless with the merge | No pre-merge gate required a green CI check before landing |
| The reviewer missed the regression | The diff spanned 40 files with no test-coverage signal in the review surface |
| The worker did not read the runbook | The runbook was not linked from the dispatch prompt and was 900 lines long |
| Someone forgot to run the validator | The validator was advisory and ran outside the commit path |
| The session should have been more careful | Detection latency was nine hours because no alert fired on a red overnight build |

The rewrite is not a euphemism.
Each right-hand entry names something that can be changed, assigned, and later observed to have changed.
