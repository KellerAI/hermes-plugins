# Andon Board Signals

The signalling half of the cord: who is paged, what state is captured at the halt, and what evidence clears the stop.

## Contents

- [The signalling contract](#the-signalling-contract)
- [Capture fields](#capture-fields)
- [Addressing the signal](#addressing-the-signal)
- [Freeze scope](#freeze-scope)
- [Clearing evidence](#clearing-evidence)
- [What never clears a stop](#what-never-clears-a-stop)
- [The pull record](#the-pull-record)

## The signalling contract

On the factory floor the cord and the board are two halves of one mechanism.
The cord stops the line; the board says which station stopped it and makes the stop visible to the person expected to walk over and answer.
A pipeline of agents needs the same split, because a halt that nobody can see is indistinguishable from an agent that quietly stalled.

The contract has four obligations.

1. The halting agent captures state before it does anything else.
2. It emits one signal, addressed to one owner, containing the trigger class, the captured state, the freeze scope, and the clearing evidence.
3. The owner acknowledges, which is a separate act from clearing.
4. The line stays down until the owner clears it against the named evidence, or the freeze widens.

An unacknowledged signal is an escalation failure and is itself recorded.

## Capture fields

Capture is mechanical and always the same shape, so that no field is skipped under pressure.

| Field | What it records | Why it matters |
| ----- | --------------- | -------------- |
| Trigger class | Which declared trigger fired | Prevents severity re-argument at fire time |
| Agent and step | Which agent halted and where in its sequence | Bounds what was and was not produced |
| Timing | When it fired relative to any file write or mutation | Distinguishes a prevented defect from a landed one |
| Premise or gate | The exact assumption, gate, or artifact at issue | The clearing evidence is written against this |
| Contradicting evidence | The observation that fired the trigger, cited by path or output | Makes the pull auditable in hindsight |
| Line state | What each sibling agent has completed, is doing, or has not started | Determines freeze scope |
| Produced artifacts | What already exists on disk or in the transcript | Determines what needs disposition |
| Freeze scope | Which agents and which downstream work are stopped | Prevents the line from restarting piecemeal |
| Escalation owner | The one person or role being paged | Without this the signal is a log line |
| Clearing evidence | What must be shown to restart, and who may accept it | Without this the stop has no exit |

Capture happens after the stop, never before.
Capturing first is how "one more step" gets finished.

## Addressing the signal

A signal is addressed to exactly one owner, chosen by trigger class from the declared catalog.

- Addressing several owners at once diffuses the obligation and reproduces the silent-dissent failure.
- Broadcasting to a channel with no named recipient is not an escalation.
- If the named owner is unavailable, the signal escalates upward to a named substitute declared with the catalog, and the line stays down in the meantime.
- The halting agent never addresses the signal to itself.

Signal shape, kept short on purpose.

```text
ANDON SIGNAL -> plan owner
Trigger ......... Contradicted assumption (declared trigger 1, halt-line)
Halted .......... wave 2 / agent w03, step 4 of 7, before any file write
Premise ......... shared contract fixes body section order at 10 sections
Evidence ........ contract revision B lists 9 sections; w01 and w02 wrote 10
Line state ...... w01 done, w02 done, w03 halted, w04 and w05 not started
Freeze .......... all wave-2 writers; wave-3 dispatch held
Clears when ..... authoritative contract revision cited by path and line, accepted
                  by the plan owner, plus a stated disposition for w01 and w02 output
```

## Freeze scope

Scope is drawn from the dependency map, not from convenience.

- Freeze the halted agent.
- Freeze every agent whose work consumes the contradicted output or shares the contradicted premise.
- Freeze the next dispatch if it was to be built on the frozen output.
- Leave running only work that provably does not touch the premise, and say in the record why it is exempt.

Scope moves in one direction while a stop is open.
New information may widen the freeze; nothing narrows it except the clear.

## Clearing evidence

Clearing evidence is named at capture time, before anyone knows how hard it will be to produce.
That ordering is the whole point — it prevents the bar from being lowered to match the effort available.

Evidence qualifies when it is:

- **Observable** — a cited file and line, a command with its exit status, an artifact at a real path.
- **Specific to the premise** — it addresses the exact assumption or gate that fired, not the general health of the work.
- **Accepted by the named owner** — acceptance is an explicit act, recorded, by the owner for that trigger class.
- **Paired with a disposition** — for a contradicted assumption, it states what happens to output already produced under the false premise: kept, reworked, or discarded.

## What never clears a stop

- Elapsed time, or a stop that expires on its own.
- Confidence, restated plans, or an assurance that the concern is probably fine.
- A second patch to the same symptom with no root cause that explains the first.
- Acceptance by the agent that pulled the cord, or by any party other than the named owner.
- The cost of the stop, however large. Sunk cost is the defect the cord exists to catch.
- Narrowing the freeze scope until the remaining work no longer touches the problem.

## The pull record

Every pull is recorded, cleared or not, and the record is the only thing that improves the catalog.

Record for each pull: the trigger class, whether it fired correctly in hindsight, how long the line was down, what the clearing evidence turned out to be, and whether the freeze scope was drawn correctly.

Two rates are worth watching together.

- A pull rate of zero across many runs means the triggers are too narrow, not that the line is clean.
- A pull rate high enough that stops are routinely overridden means the triggers are too broad, and the cord is being trained out of the pipeline.

False pulls are recorded without penalty.
The moment a false pull costs the puller something, the next true one is swallowed, and the board goes dark exactly when it is needed.
