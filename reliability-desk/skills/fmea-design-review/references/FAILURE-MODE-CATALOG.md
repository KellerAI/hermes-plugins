# Failure Mode Catalog

A starter catalog of recurring failure modes in agent systems, data pipelines, and service code.
Use it to seed enumeration after the function list exists — never as a replacement for enumerating against the actual design.
A mode from this catalog earns a row only when it maps to a named function in the artifact under review.

## Contents

- [Data and state modes](#data-and-state-modes) — how stored or in-flight data goes wrong.
- [Control-flow and retry modes](#control-flow-and-retry-modes) — how execution goes wrong.
- [Boundary and integration modes](#boundary-and-integration-modes) — how the edges between systems go wrong.
- [Agent-specific modes](#agent-specific-modes) — how an LLM-driven workflow goes wrong.
- [Observability modes](#observability-modes) — how the failure stays invisible.
- [Using the catalog](#using-the-catalog) — the mapping rule and the trap to avoid.

## Data and state modes

| Mode | What it looks like | Typical effect to write down |
| ---- | ------------------ | ---------------------------- |
| Silent truncation | Output is cut at a limit and returned without an error | Downstream consumes a partial record as if complete |
| Partial write | A multi-step write applies some steps and abandons the rest | State is internally inconsistent and no marker says which half landed |
| Stale cache read | A cached value is returned after the source changed | Users act on data that is quietly out of date |
| Lost update | Two writers read, modify, and write the same record | The second write erases the first with no conflict raised |
| Schema drift | Producer changes a field the consumer still expects | Consumer parses successfully into the wrong shape |
| Encoding mismatch | Bytes decoded under the wrong assumption | Text corrupts in a way that survives validation |
| Unbounded growth | A table, queue, or log grows without a retention rule | Capacity exhaustion at an unrelated time |

## Control-flow and retry modes

| Mode | What it looks like | Typical effect to write down |
| ---- | ------------------ | ---------------------------- |
| Unbounded retry | Failures retried without a cap or backoff | The dependency's slow period becomes an outage |
| Non-idempotent retry | A retried call repeats a side effect | Duplicate charges, duplicate rows, duplicate notifications |
| Timeout mismatch | Caller times out before the callee finishes | Work completes but the caller records failure |
| Silent fallback | An error path returns a default that looks valid | Wrong answers with no error signal anywhere |
| Fail-open guard | A check errors and the request proceeds | The control that existed to block is bypassed exactly when it was needed |
| Ordering assumption | Concurrent steps assumed to complete in written order | Intermittent, unreproducible wrongness |
| Deadlock or livelock | Two paths wait on each other, or spin without progress | Throughput drops to zero with no error raised |

## Boundary and integration modes

| Mode | What it looks like | Typical effect to write down |
| ---- | ------------------ | ---------------------------- |
| Unvalidated input | External data trusted at the boundary | Malformed or hostile input reaches internal logic |
| Version skew | Two deployed components disagree on a contract | Requests succeed against one instance and fail against another |
| Credential expiry | A token or certificate lapses unnoticed | Total loss of an integration at an unpredictable moment |
| Rate-limit collision | Aggregate callers exceed a shared quota | An unrelated caller is throttled and blamed |
| Partial dependency outage | A dependency degrades rather than failing | Health checks stay green while user work fails |

## Agent-specific modes

| Mode | What it looks like | Typical effect to write down |
| ---- | ------------------ | ---------------------------- |
| Unverified self-report | An agent reports completion it never observed | A false claim enters the record as fact |
| Context truncation | Earlier instructions fall out of the window | Later steps contradict constraints already agreed |
| Tool-output misparse | Structured output read under the wrong assumption | A confident action taken on a misread result |
| Scope creep after approval | Work expands past what was confirmed | Unreviewed changes land alongside reviewed ones |
| Mocked path passing as real | A test asserts against a stub | Green signal with zero coverage of the real behaviour |
| Ephemeral write loss | Output written into a location torn down afterwards | The deliverable does not exist despite a success report |

## Observability modes

| Mode | What it looks like | Typical effect to write down |
| ---- | ------------------ | ---------------------------- |
| Swallowed exception | An error caught and discarded | The failure leaves no trace to detect |
| Alert without a receiver | An alarm routed to an unread channel | Detection exists on paper and not in practice |
| Success masked by a pipe | A non-zero exit hidden behind a later command | A failing step is cited as a passing one |
| Metric without a denominator | A count reported with no base to compare it against | The number cannot indicate whether anything is wrong |

## Using the catalog

Map each candidate mode to one named function before scoring it.
The trap is mode inflation: importing thirty catalog rows makes the table look thorough while pushing the real item down the ranking and diluting every score.
Import only the modes the artifact can actually exhibit, and say in the output which catalog sections you swept.
