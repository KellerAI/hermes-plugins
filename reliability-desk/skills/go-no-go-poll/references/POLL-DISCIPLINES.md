# Poll Disciplines

The default roster for a software release poll, adapted from the console-by-console launch poll.
Each discipline owns one scope, answers for that scope only, and must cite evidence with its call.

## Roster

| Discipline | Scope owned | Evidence required with the call |
| ---------- | ----------- | ------------------------------- |
| Correctness | The release behaves as specified | Test and eval results tied to the candidate revision, or a named manual check with its outcome |
| Security | Secrets, credentials, permissions, and newly exposed surface | Scan output, or an explicit statement of the surface reviewed and what changed |
| Data and migrations | Schema changes, stored data, and the reverse path for both | The migration plan, the down-migration, and whether either has been exercised |
| Operability and rollback | Deploying, observing, and reversing the release in production | The rollback procedure and evidence it was rehearsed, plus the signal that would trigger it |
| Documentation | What users are told the release does | Changelog and user-facing documentation compared against the actual diff |

## Answering rules

Each owner answers exactly one of GO, NO-GO, or NO-GO pending.
NO-GO pending means the work to reach a call is identified but not finished; it holds the release exactly as a NO-GO does.
No owner answers for a scope they do not own, and no owner answers for another person.

When one operator covers several disciplines, they answer once per discipline with separate evidence for each.
The record must state that the disciplines shared an owner, so a later reader can see where independence was thin.

## Adding and removing disciplines

Add a discipline when the release touches a scope no seated console owns.
Common additions are cost and quota, third-party dependencies and licensing, and regulatory or privacy review.

Remove a discipline only when its scope is provably untouched by this release, and record the reason in the poll.
Dropping a console because the release is late is roster shrinkage, not scoping.

## Evidence quality

A cited artifact beats a recollection.
An artifact tied to the exact candidate revision beats one from an earlier build.
An exercised path beats a documented path.
A GO with no cited artifact is an opinion and should be returned to the owner as unanswered.
