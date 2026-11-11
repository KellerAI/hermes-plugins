# Emergency Change Path

The emergency class exists so that an outage is not prolonged by a queue.
It does not exist to bypass the record.
This file states what an emergency change may skip, what it may never skip, and the retroactive-review obligation it incurs.

## Entry conditions

An emergency change is available only when production impact is happening now, the delay of normal review measurably worsens that impact, and the proposed change is the narrowest action that addresses it.
If any one of the three fails, the change is normal, however urgent it feels.

## What an emergency change may skip

- The scheduling window or change freeze.
- The queued reviewer and any wait for their availability.
- Pre-merge sign-off from parties who are not required to execute the fix.
- Batching with other pending work.
- Documentation polish that can be completed after impact ends.

## What an emergency change may never skip

- The record — a change with no record did not happen under this protocol.
- The named human actor — "the on-call" is not a name, and the agent is never the actor of record.
- The stated impact that justified the class.
- The itemised list of normal-change steps that were skipped.
- The reversal path, even if the reversal is "revert the commit".
- The retroactive-review owner and deadline.
- Any control that exists to prevent irreversible loss, such as taking a backup before a destructive migration.

The last item is the one most often lost under pressure.
Speed may buy out review; it may not buy out recoverability.

## Narrowness

An emergency change carries only what the impact requires.
Refactors, dependency bumps, formatting, and unrelated fixes travelling alongside the fix are not emergency changes and must be split out.
If the fix cannot be separated from the surrounding work, say so in the record and treat the whole payload's blast radius as the emergency's blast radius.

## The retroactive-review obligation

Every emergency change creates one open obligation.
It is closed by a review that answers four questions:

1. Was the emergency class correctly assigned, given what is now known?
2. Did the change actually resolve the impact, and did it introduce anything new?
3. Which skipped steps would have caught a defect, had they run?
4. What would make this class of change a standard or normal change next time?

Ownership rules:

- The owner is a named individual, recorded at the moment the emergency is declared, not chosen later.
- The owner should not be the person who executed the change where an alternative exists.
- The deadline is a date, set at declaration, and it is short — measured in days, not quarters.
- The obligation is tracked where open work is tracked, not only inside the record file.

## Closing the loop

A retroactive review that finds the class was wrong does not punish the actor; it corrects the criteria.
A recurring emergency of the same shape is evidence that a pre-approved standard pattern is missing, and creating that pattern is the correct output of the review.
An emergency record whose review deadline has passed with no review is an overdue control failure and should be escalated as one.
