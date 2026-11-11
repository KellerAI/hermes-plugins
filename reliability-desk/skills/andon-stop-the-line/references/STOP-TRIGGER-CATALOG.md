# Stop-Trigger Catalog

Candidate halt triggers for a pipeline of agents, with the severity that justifies each and the owner who answers the cord.
Copy the rows that apply to your line, delete the rest, and declare the result before the line starts.

## Contents

- [How to use this catalog](#how-to-use-this-catalog)
- [Severity bands](#severity-bands)
- [Trigger classes](#trigger-classes)
  - [Failing gate](#failing-gate)
  - [Contradicted assumption](#contradicted-assumption)
  - [Missing evidence](#missing-evidence)
  - [Unexpected destructive step](#unexpected-destructive-step)
  - [Repeated identical failure](#repeated-identical-failure)
  - [Scope divergence between siblings](#scope-divergence-between-siblings)
  - [Silent capability loss](#silent-capability-loss)
- [Non-triggers](#non-triggers)
- [Declaring the catalog for a run](#declaring-the-catalog-for-a-run)

## How to use this catalog

A trigger is usable only when it is observable, ownable, and clearable.
Observable means a specific agent can tell that it fired without a judgement call about severity.
Ownable means one named person or one orchestrator role answers when it fires.
Clearable means there is a piece of evidence that, if produced, permits the line to restart.

A candidate trigger that fails any of the three is either rewritten until it passes or left out.
Carrying an unusable trigger is worse than carrying none, because it teaches the line that the catalog is decorative.

## Severity bands

| Band | Meaning | Line behaviour |
| ---- | ------- | -------------- |
| Halt-line | The defect is upstream of work in flight; downstream output is already suspect | Stop the halted agent and every consumer of its output |
| Halt-agent | The defect is contained to one agent's own scope | Stop that agent; siblings continue and are told what fired |
| Flag | The defect is real but nothing in flight depends on it | No stop; recorded and carried to backlog |

Band assignment happens when the catalog is declared, not when the trigger fires.
A trigger whose band is argued at fire time is an unowned trigger with extra steps.

## Trigger classes

### Failing gate

Fires when a required test, lint, schema, policy, or validation gate fails and a downstream step would otherwise proceed.

- Typical band: halt-line when the gate covers a shared artifact, halt-agent when it covers one agent's own file.
- Default owner: the orchestrator.
- Clearing evidence: the gate re-run and observed green, cited by command and exit status, on the same revision the line will continue from.
- Note: a gate that was skipped is a missing-evidence trigger, not a failing-gate trigger.

### Contradicted assumption

Fires when any agent finds evidence that a load-bearing premise of the shared plan is false.

- Typical band: halt-line, always. A premise is shared by definition.
- Default owner: the plan owner.
- Clearing evidence: the authoritative source cited by path and line, plus a stated disposition for output already produced under the old premise.
- Note: the disposition is part of the clearing evidence. Restarting without saying what happens to the work built on the false premise leaves the scrap in the pipeline.

### Missing evidence

Fires when a step is asked to certify something it cannot observe, or when a cited artifact does not exist at the cited path.

- Typical band: halt-agent, escalating to halt-line if the missing artifact is one other agents were told to read.
- Default owner: the verifying owner — whoever asked for the certification.
- Clearing evidence: the artifact produced at a real path, or the certification requirement withdrawn in writing.
- Note: an agent that certifies anyway is committing the failure this trigger exists to catch, and the pull must be recorded against the certification, not the artifact.

### Unexpected destructive step

Fires when work reaches an operation that mutates, deletes, publishes, or force-pushes outside the scope declared at the start of the line.

- Typical band: halt-line.
- Default owner: the human operator. This class is never cleared by an agent.
- Clearing evidence: explicit operator authorization naming the exact operation and its scope.
- Note: the halt precedes the operation. A trigger that fires after the mutation is a post-mortem, not a cord.

### Repeated identical failure

Fires when the same failure recurs after a fix was applied, indicating the diagnosis was wrong rather than the fix incomplete.

- Typical band: halt-agent on the second occurrence, halt-line on the third.
- Default owner: the plan owner.
- Clearing evidence: a stated root cause that explains both occurrences, not a second patch.
- Note: this is the handoff point to a structured debugging workflow. Andon stops the line; it does not diagnose.

### Scope divergence between siblings

Fires when two agents on the same wave produce output that cannot both be correct — conflicting structure, contradictory findings, or incompatible interpretations of the same instruction.

- Typical band: halt-line for the affected wave.
- Default owner: the orchestrator.
- Clearing evidence: one interpretation selected on the record, plus a rework instruction for the agent whose output is superseded.

### Silent capability loss

Fires when an agent loses a tool, permission, or data source it was expected to use and continues on a degraded path without saying so.

- Typical band: halt-agent, escalating if the degraded output has already been consumed.
- Default owner: the orchestrator.
- Clearing evidence: the capability restored and the affected step re-run, or the degraded path explicitly accepted with its limitation recorded.

## Non-triggers

These are recorded and carried, never halted on, unless they intersect work in flight.

- Cosmetic lint or formatting warnings in files no agent in the current run is editing.
- Pre-existing issues in untouched code discovered incidentally during a search.
- Style disagreements that do not change behaviour or contradict a declared premise.
- Performance observations without a stated threshold that has been crossed.
- Anything whose only justification is that it feels unfinished.

## Declaring the catalog for a run

Write the selected triggers in one block before dispatch, in this shape.

```text
LINE: docs-refresh wave 2, five parallel writer agents
TRIGGERS DECLARED:
  1. Contradicted assumption ....... halt-line  ... owner: plan owner
  2. Unexpected destructive step ... halt-line  ... owner: human operator
  3. Missing evidence .............. halt-agent ... owner: orchestrator
  4. Scope divergence .............. halt-line  ... owner: orchestrator
NON-TRIGGERS: lint warnings outside owned files; pre-existing issues in untouched plugins
CLEARING AUTHORITY: named owner only; elapsed time never clears a stop
```

Any trigger not in the declared block is a flag, and any trigger in the block fires on its own terms without a severity re-argument at fire time.
