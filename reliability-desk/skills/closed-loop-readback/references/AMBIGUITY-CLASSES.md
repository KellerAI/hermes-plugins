# Ambiguity Classes

The four recurring classes of instruction ambiguity, the question each one obliges the readback to force, and how to tell when the class is present.

## Contents

- [Class 1 — Unnamed Target](#class-1--unnamed-target)
- [Class 2 — Unstated Scope Boundary](#class-2--unstated-scope-boundary)
- [Class 3 — Undefined Done-Condition](#class-3--undefined-done-condition)
- [Class 4 — Implied Destructive Step](#class-4--implied-destructive-step)
- [Quick Reference](#quick-reference)
- [When Two Classes Fire at Once](#when-two-classes-fire-at-once)

## Class 1 — Unnamed Target

The instruction names a category rather than an object.

**Signals:** a collective noun ("the tests", "the config", "the docs"), a demonstrative with no antecedent ("fix this"), or a role name where a path is needed ("the entry point").

**Why it is dangerous:** the receiver silently resolves the category to whichever member is most salient to them, which is rarely the one most salient to the sender.
The divergence surfaces only after the wrong file has been edited.

**Question the readback must force:** exactly which named objects are in the set, enumerated, with nothing left to inference.

Enumerate the resolved set in the in-scope block.
If the set has more than roughly ten members, state the rule that generated it as well as the count, so the sender can check the rule rather than the list.

## Class 2 — Unstated Scope Boundary

The instruction says where to start and never says where to stop.

**Signals:** "all", "everywhere", "while you're in there", "and anything similar", or an instruction that names an operation with no delimiter at all.

**Why it is dangerous:** the receiver's boundary is an invention, and an invented boundary is usually wider than the sender's.
Over-broad work is harder to review, harder to revert, and hides the intended change inside noise.

**Question the readback must force:** what adjacent work is deliberately excluded, stated as its own list rather than implied by omission.

The out-of-scope list is the load-bearing half of this class.
A readback that only says what is included does not test the boundary; it merely asserts one.

## Class 3 — Undefined Done-Condition

The instruction describes an activity rather than an end state.

**Signals:** "clean up", "improve", "tighten", "make it better", "look into" — verbs whose completion is a judgement call.

**Why it is dangerous:** without an observable, neither party can disagree about whether the work finished, so the receiver declares completion unilaterally and the sender discovers later that the bar was elsewhere.

**Question the readback must force:** the single observable that will be true when the work is done, phrased so that a third party could check it without asking either participant.

One criterion, not several.
Multiple criteria let a partially finished task be declared complete against the easiest one.
If the work genuinely has several end states, that is a signal the instruction should be split into several instructions, each with its own loop.

## Class 4 — Implied Destructive Step

The instruction requires an irreversible action that it never mentions.

**Signals:** "drop", "clean", "reset", "start fresh", "get rid of", "consolidate", "replace" — any verb whose ordinary implementation deletes, overwrites, force-pushes, or discards state.

**Why it is dangerous:** the destructive step is the part the sender would most want to veto and the part the instruction is least likely to spell out.
It is also the only class where a wrong readback cannot be undone by a follow-up edit.

**Question the readback must force:** name the destructive operation outright, name what it will destroy, and state whether the loss is recoverable.

This class is never omitted from a readback on grounds of obviousness.
Where a destructive step conflicts with a stated constraint — "delete the branches but lose no work" — the readback states which clause binds and stops rather than resolving the conflict silently.

## Quick Reference

| Class | Signal | Question the readback must force |
| ----- | ------ | -------------------------------- |
| Unnamed target | Collective noun or bare demonstrative | Which named objects are in the set? |
| Unstated scope boundary | "all", "everywhere", no delimiter | What adjacent work is explicitly excluded? |
| Undefined done-condition | Judgement verb, no end state | What single observable ends this task? |
| Implied destructive step | Delete, reset, replace, consolidate | What exactly is destroyed, and is it recoverable? |

## When Two Classes Fire at Once

Most real instructions carry two or three classes together.
"Clean up the stale stuff" fires unnamed target, undefined done-condition, and implied destructive step simultaneously.

Answer them in the order above.
Resolving the target first is what makes the boundary checkable, the boundary is what makes the done-condition observable, and the destructive step can only be named accurately once the target set is fixed.

When more than two classes fire and the readback would need more assumptions than facts, that is the boundary of this skill.
Escalate as an owned question to the named owner: the answer does not exist yet and needs a named owner to supply it, not a confirmation to close the loop.
