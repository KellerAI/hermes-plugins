# Change Classes

The three classes, the criteria that select each one, the approver each requires, and the record each leaves behind.
Assign exactly one class per change.
When a change plausibly fits two classes, take the higher one — the order is standard, then normal, then emergency.

## Standard change

A standard change is one whose risk has already been assessed and pre-approved as a repeatable pattern.

Criteria — all must hold:

- The change matches a named pre-approved pattern that someone previously classified.
- It is reversible in place, without a data migration or a restore.
- It touches no authentication, authorisation, secret, billing, or personal-data path.
- It does not alter a published interface that other systems depend on.
- Its failure mode is visible immediately rather than silently corrupting state.

Approver: the standing pre-approval itself.
No individual signs a standard change.

Required record: the class and the name of the pre-approved pattern it matched.
That is the whole record.

If no pre-approved pattern exists yet, the change is not standard.
Creating a new pattern is itself a normal change.

## Normal change

A normal change is the default.
Anything that is not a matched pre-approved pattern and is not an active incident response is normal.

Criteria — any one is sufficient:

- The change is not covered by an existing pre-approved pattern.
- Reversal requires a migration, a restore, or a coordinated rollback.
- It touches an auth, secret, billing, or personal-data path.
- It changes a published interface, a schema, or a default.
- Its blast radius cannot be stated confidently in one sentence.

Approver: a named reviewer who is not the author.
Naming a team is not naming a reviewer.

Required record:

- The class.
- The blast radius: which systems, which data, which users.
- The reversal path, stated concretely.
- The named reviewer.
- Any conditions attached to the approval, written as verifiable statements.

## Emergency change

An emergency change is a response to active production impact where waiting for review costs more than proceeding.

Criteria — all must hold:

- There is impact happening now, not impact anticipated later.
- The delay imposed by normal review measurably worsens that impact.
- The change is the narrowest action that addresses the impact.

A deadline is not an emergency.
A release date is not an emergency.
Discovering the work late is not an emergency.

Approver: the named human taking the action, on the record, by name. The agent is never the approver or actor of record.
This is a deliberate solo-operator adaptation; ITIL routes emergency changes through a designated emergency change authority rather than the actor alone.

Required record:

- The class and the impact that justified it.
- Which normal-change steps were skipped, itemised.
- The named retroactive-review owner.
- The retroactive-review deadline, as a date.

## Escalation and de-escalation

A change may be escalated at any point before merge when new facts widen its blast radius.
A change may only be de-escalated by the approver of the higher class, and the de-escalation is itself recorded.
Never de-escalate a change to make a gate easier to pass.

## Quick selection

| Question | If yes |
| -------- | ------ |
| Is production impacted right now, and does waiting make it worse? | Emergency |
| Does it match a named pre-approved pattern with no auth, data, or interface exposure? | Standard |
| Anything else | Normal |
