# Contributing Factors Taxonomy

The six categories a blameless review sweeps before it writes any action, so coverage comes from the procedure rather than from what the reviewer happened to notice.

## How to Use It

Walk every category in order, even the ones that look irrelevant.
Record a finding or the words "no contribution found" for each; a silently skipped category is indistinguishable from a clean one.
No category is allowed to resolve to a person — if a sweep produces "the operator", re-run the substitution test and rewrite the finding as a condition.

## The Categories

| Category | What to look for | Where the evidence lives |
| -------- | ---------------- | ------------------------ |
| Prompt and acceptance-criteria defects | Instructions that were ambiguous, under-specified, or that accepted a self-report as evidence; a done-condition that was not observable | The dispatch prompt, the kickoff or brief file, the issue text, the transcript's first turns |
| Tool-surface gaps | A capability the operator needed and did not have, a tool that failed silently, or a surface so wide the wrong tool was reachable | Skill and agent `allowed-tools`, the session tool surface, tool-call errors in the transcript |
| Guard and hook coverage | A rule that was advisory when it needed to be blocking, a gate that ran too late, or a path that bypassed enforcement entirely | Hook configuration, lefthook and CI workflow files, guard denial and advisory messages |
| Handoff and context loss | State that existed in one session and not the next; a worktree, branch, or artifact whose location was never transferred | Handoff documents, `git log` across branches, mail or hub threads, the boundary between sessions |
| Time pressure and load | Work compressed to beat a deadline, batches sized past the point where verification fits, concurrency that starved a check | Timestamps in `git log` and the transcript, batch sizes, the number of items in a single dispatch |
| Detection latency | How long the failure ran before anything noticed, and what would have noticed sooner | Failure timestamp versus first alert or first human report, monitoring and alert configuration |

## Reading the Sweep

Categories interact, and the interaction is usually the story.
A prompt defect that would have been harmless with a blocking gate becomes an incident when the gate is advisory and detection is measured in hours.
State the interaction explicitly rather than filing three unrelated findings that each look survivable on their own.

Every category that produced a finding must produce at least one systemic action, or the review must state why the condition is being accepted as-is and who accepted it.
