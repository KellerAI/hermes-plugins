# Readback Templates

The three-part readback shape, plus worked rewrites for the three instruction defects that most often reach an agent.

## Contents

- [The Three-Part Shape](#the-three-part-shape)
- [What Counts as "Own Words"](#what-counts-as-own-words)
- [Rewrite 1 — The Vague Instruction](#rewrite-1--the-vague-instruction)
- [Rewrite 2 — The Over-Broad Instruction](#rewrite-2--the-over-broad-instruction)
- [Rewrite 3 — The Internally Contradictory Instruction](#rewrite-3--the-internally-contradictory-instruction)
- [Reading Back a Correction](#reading-back-a-correction)

## The Three-Part Shape

Air traffic phraseology closes a loop in three moves: the sender transmits, the receiver reads the operative content back, and the sender confirms or corrects.
Only the third move completes delivery.
Adapted to an agent instruction, the three parts become:

1. **Transmit** — the user's instruction as issued, however under-specified.
2. **Read back** — the receiver's own-words restatement, carrying scope in, scope out, one done-condition, and every assumption.
3. **Confirm or correct** — the sender's `confirm` (proceed exactly as read back) or `correct` (amend, then read back again).

The operative content is what would change the outcome if it were wrong.
Courtesy phrasing, rationale, and background are not read back; targets, boundaries, done-conditions, and destructive steps always are.

## What Counts as "Own Words"

A restatement passes when at least two of the following are true against the original:

- Different sentence structure, not a word-level substitution.
- Pronouns and demonstratives ("this", "that one", "the usual place") replaced by named targets.
- Vague collective nouns ("the config", "the tests", "everything") replaced by an enumerated list.
- An implication made explicit that the sender left implicit.

A restatement fails when it is the original sentence with synonyms swapped.
That form proves the message arrived; it does not prove it was understood.

## Rewrite 1 — The Vague Instruction

**Instruction:** "Clean up the config in this repo."

The defect is an unnamed target and an undefined done-condition.
"Clean up" names no operation, and "the config" names no file.

```text
READBACK — no action taken yet.

As I understand it, you are asking me to reduce duplication and remove dead
entries across the repository's configuration files, without changing any
behaviour that those files currently produce.

In scope:
- `.markdownlint-cli2.yaml`
- `lefthook.yml`
- `.editorconfig`

Explicitly out of scope:
- Any file under `plugins/` (including per-plugin manifests)
- Any change that alters which hooks run or when

Success criterion (one observable):
- Every hook that ran before the change still runs, with identical inputs,
  and no configuration key has changed value.

Assumptions I am making:
- "Config" means repository tooling config, not application settings.
- Reformatting is acceptable; re-keying is not.
- No configuration file is generated from another source.

I have taken no action and will take none until you reply.
Reply `confirm` to proceed exactly as read back, or `correct` with the change.
```

The rewrite converts one adjective into three named files, one behavioural invariant, and three assumptions the sender can veto in a single word.

## Rewrite 2 — The Over-Broad Instruction

**Instruction:** "Fix all the lint errors."

The defect is an unstated scope boundary.
"All" spans files nobody asked to touch, and a repo-wide sweep buries the change the sender actually wanted.

```text
READBACK — no action taken yet.

As I understand it, you are asking me to resolve the markdownlint violations
in the files changed on this branch, leaving pre-existing violations elsewhere
in the repository untouched.

In scope:
- The 4 Markdown files modified on this branch

Explicitly out of scope:
- Markdown files this branch did not touch
- Any lint rule change or suppression comment
- Any non-Markdown linter

Success criterion (one observable):
- `markdownlint-cli2` exits 0 for the 4 changed files.

Assumptions I am making:
- "All" is scoped to this branch, not the repository.
- Fixing means editing the content, not disabling the rule.
- Peer-owned dirty files are not mine to touch.

I have taken no action and will take none until you reply.
Reply `confirm` to proceed exactly as read back, or `correct` with the change.
```

The out-of-scope line does the work here: it forces the sender to notice, before any edit lands, that a repo-wide interpretation was available and was declined.

## Rewrite 3 — The Internally Contradictory Instruction

**Instruction:** "Drop the stale branches but don't lose any work."

The defect is a contradiction between the operation and the constraint, plus an implied destructive step.
Deleting branches can lose commits; the two clauses cannot both hold unconditionally.

```text
READBACK — no action taken yet.

As I understand it, you are asking me to delete local branches whose commits
are already contained in `origin/main`, and to leave untouched any branch
carrying a commit that exists nowhere else.

In scope:
- Local branches fully merged into `origin/main`

Explicitly out of scope:
- Any branch with commits absent from `origin/main`
- Any remote branch
- Any commit, stash, or worktree

Success criterion (one observable):
- Every commit reachable before the change is still reachable after it.

Assumptions I am making:
- "Stale" means merged, not old by date.
- This is a destructive step: branch refs will be deleted.
- Losing no work is the binding constraint; where the two clauses conflict,
  I stop rather than delete.

I have taken no action and will take none until you reply.
Reply `confirm` to proceed exactly as read back, or `correct` with the change.
```

The contradiction is not resolved silently.
It is resolved in the open, by naming which clause binds, so the sender can overrule that ranking before anything is deleted.

## Reading Back a Correction

A `correct` reply is a new transmission and gets a new readback.
Carry forward the parts that were not corrected, mark the changed part, and wait again.

```text
READBACK (revision 2) — no action taken yet.

Correction absorbed: scope is the repository, not this branch.

<remaining sections restated in full>

I have taken no action and will take none until you reply.
Reply `confirm` to proceed exactly as read back, or `correct` with the change.
```

Restate every section in full on a revision.
A revision that shows only the delta forces the sender to reassemble the instruction from two messages, which is the reassembly error the loop exists to catch.
