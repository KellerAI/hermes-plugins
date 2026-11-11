# Three-Gate Structure

Each gate has a question set, a named answerer, and a blocking condition.
A gate that cannot block is not a gate.

## Gate 1 — Sign-in

Runs before any MUTATING action is proposed.
The read-only inspection needed to enumerate scope and record the starting tree state is part of sign-in, not a bypass of it.

**Asks:**

- What is this session for, in one sentence?
- Which files may be touched, listed by path?
- What is the rollback path if the session goes wrong?
- Who owns this session?
- What is the working tree's starting state?

**Answered by:** the operator running the session, out loud in the transcript.

**Blocks when:**

- The scope sentence contains "and also" or otherwise names two unrelated goals.
- The file list is open-ended ("whatever needs changing").
- No rollback path exists, or the named path depends on something not yet created.
- A dirty file is neither claimed by this session nor recognised as peer work to be left untouched.

**Passing record:** scope sentence, file list, rollback path, owner, starting state.

## Gate 2 — Time-out

Runs immediately before the first mutating action, and again after any plan change.

**Asks:**

- What are the ordered steps?
- Which files does each step touch?
- What observable result should each step produce?
- What does this plan assume that has not been verified?
- Does the user confirm this plan as stated?

**Answered by:** the operator states the plan; the user gives the confirmation.
The confirmation may not be inferred, assumed, or supplied by the same party that proposed the plan.

**Blocks when:**

- No explicit confirmation has been received.
- The plan touches a file absent from the sign-in list.
- A stated assumption is load-bearing and unverified.

**Passing record:** the plan as stated, the assumptions listed, the confirmation quoted.

## Gate 3 — Sign-out

Runs before the session ends, including when it ends early, is interrupted, or hands off.

**Asks:**

- Which files actually changed?
- How does that differ from the sign-in list?
- Which changes have not been observed to work, and what check would verify each?
- What does the next session inherit, and who owns each open item?
- What state is the working tree in right now?

**Answered by:** the operator, against observed evidence rather than intent.

**Blocks when:**

- A change is unverified and does not appear on the unverified list.
- A file changed that never appeared on the sign-in list and the divergence is unexplained.
- The working-tree state is not stated.

**Passing record:** the changed list, the unverified list, the handoff list, the tree state.

## Ordering Rules

- Gates run in order and never out of order.
- A later gate cannot pass while an earlier one is held.
- Expanding scope mid-session returns the session to sign-in.
- A single gate may be run alone when the user asks for it, but running one gate does not satisfy the others.
- A held gate is a stop, not a warning.
