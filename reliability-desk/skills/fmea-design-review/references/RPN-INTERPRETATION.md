# RPN Interpretation

How to read the Risk Priority Number honestly, when severity overrides the ranking, and how to re-score after mitigation.

The 2019 AIAG-VDA handbook replaced RPN with Action Priority tables; RPN remains the working form in SAE J1739 and in most practice, and this skill keeps it for its transparency.

## RPN is ordinal, not probabilistic

RPN is the product of three ordinal ranks: `S x O x D`.
Ordinal ranks carry order but not distance, so their product carries neither.
An RPN of 240 is not twice as risky as an RPN of 120, and neither number expresses a probability of anything.

What RPN legitimately supports:

- Deciding which mode to work on next.
- Showing that two reviewers disagree about one specific dimension rather than about the whole design.
- Demonstrating that a mitigation moved a named score.

What RPN never supports:

- A statement of absolute risk, a failure rate, or an expected loss.
- Comparison against another team's table scored on different anchors.
- A threshold claim such as "everything under 100 is acceptable", which is arithmetic dressed as a risk appetite.

Say the limitation in the output.
A table presented without it invites the reader to treat 240 as a measurement.

## Why the product hides things

The product is symmetric: a 10 in one dimension is arithmetically identical to a 10 in another.
That is exactly wrong for severity, because severity describes harm that has already happened by the time the mode fires, while occurrence and detection describe the chance of getting there.

Worked comparison:

| Mode | S | O | D | RPN |
| ---- | - | - | - | --- |
| Silent corruption of a committed ledger batch | 10 | 1 | 2 | 20 |
| Timestamp renders in the wrong timezone label | 3 | 8 | 4 | 96 |

The cosmetic defect outranks the data-corruption mode by a factor of nearly five.
Ranking by RPN alone and stopping there is the standard false negative of this practice.

## The severity override

Apply this rule on every table.

- Any mode scoring S of 9 or 10 is escalated regardless of its RPN.
- Escalated modes are listed above the RPN ordering, each with a stated reason the effect is intolerable.
- The escalation is not deleted by a low occurrence or a low detection score; those may shape the mitigation, never the escalation.

A secondary rule worth applying: any mode with D of 10, meaning no control could observe it at all, is called out separately even when its RPN is low.
An unobservable mode's occurrence score is an estimate with no evidence behind it, because nothing was ever positioned to count it.

## Comparing within one table only

Scores are meaningful relative to the anchors declared for that review.
Two tables scored on different anchors are not comparable, and averaging RPN across a portfolio produces a number with no referent.
If a programme-level view is needed, count modes by severity band instead.

## The re-scoring rule

Re-scoring is how the table stays alive after the review.

1. Record the original S, O, D, and RPN unchanged.
   Never overwrite them.
2. Record the projected re-scored RPN in its own column, and mark it projected.
3. State which dimension the mitigation moves and why: reduced occurrence, improved detection, or reduced severity through a design change.
4. A projection becomes an actual score only when the mitigation exists and has been observed working.
   Until then it is a plan.
5. Severity is re-scored only when the design changed.
   Adding monitoring improves detection and leaves severity where it was.

Marking a projected RPN as achieved before the mitigation is built converts a plan into a false claim, and it is the point at which an FMEA stops being evidence.

## When to stop the review

Stop when every function has been swept with all five mode classes, every S of 9 or 10 has an owner and an action, and at least one mitigation improves detection.
Do not stop because the table reached a row count, and do not keep going to make the table look comprehensive.
Rows added past the point of discrimination lower every score's information content.
