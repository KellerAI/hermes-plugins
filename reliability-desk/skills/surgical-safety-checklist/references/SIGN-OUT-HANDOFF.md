# Sign-Out Handoff

The sign-out record is three separate lists that are never merged.
Merging them is how unverified work gets reported as finished.

## List 1 — Changed

One row per file actually modified, created, or moved during the session.

- Cite the path exactly as it appears in the repository.
- State what changed in that file in one clause.
- Mark whether the path appeared on the sign-in list.
- Any path not on the sign-in list carries a one-sentence explanation of why scope expanded.

The changed list is built from observed evidence — `git status` and `git diff` output the user shares, or the write operations recorded in the transcript — never from the plan.
A file that the plan intended to change but did not is absent from this list.

## List 2 — Unverified

One row per change whose correctness was not observed during the session.

- Name the change.
- Name the specific check that would verify it: a command, a test, a manual observation.
- State why it was not run: out of scope, blocked, expensive, forgotten.
- Assign an owner for running it.

Rules that keep this list honest:

- A change is verified only when a check was actually run and its result observed.
- A passing lint or a clean working tree is not verification of behaviour.
- "Looks right" is not an observation and belongs on the unverified list.
- An empty unverified list is a strong claim and must be defensible change by change.

## List 3 — Handed Off

What the next session inherits, whether that session is the same operator an hour later or a different one.

- Open items with an owner each.
- Decisions taken during the session that constrain later work.
- Decisions deliberately deferred, and to whom.
- The working-tree state: clean, dirty with named files, on which branch, committed or not.
- Anything running or half-applied that a later session must not assume is settled.

## Anti-Patterns Specific to Sign-Out

- Collapsing unverified into handed-off, which buries risk inside a to-do list.
- Reporting the plan as the changed list.
- Ending a session that was interrupted without signing out, on the grounds that it was not finished.
- Omitting the tree state, which forces the next session to rediscover it.
- Listing an unverified item with no owner, which is the same as dropping it.

## Minimum Viable Sign-Out

When the session must end abruptly, the irreducible record is: what changed, what is unverified, and what state the tree is in.
Those three facts take under a minute and prevent the failure the gate exists to catch.
