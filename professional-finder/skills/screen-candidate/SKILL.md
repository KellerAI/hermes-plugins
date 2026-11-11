---
name: screen-candidate
description: Use before engaging or making an offer to a licensed professional, when the user wants a full credential report, disciplinary history, or a public-record check of someone's professional license and regulator record. Runs license verification plus profession-specific regulator checks, flags red flags with sources, and returns a dated credential report. Not a background check and not a consumer report.
license: Apache-2.0
---

# Screen a candidate (credential report)

**Load `professional-finder:ground-rules` first and follow it throughout.** Its hard rules, FCRA and anti-discrimination cautions and output conventions apply to every step below.

A deeper, documented look at a professional's **license and regulator record** before the user engages them. This folds in the former "license investigator" role: you run it end to end and return one report.

Read the FCRA and anti-discrimination cautions in `professional-finder:ground-rules` first. In short: this is not a background check, not a consumer report, and never a basis for an adverse employment action. No criminal, arrest, credit, bankruptcy, eviction or civil-court searches about an individual. Only job-related professional criteria.

## Layer 1: License verification

Run `verify-license` for every license the role needs, in every state where the work happens.

## Layer 2: Regulator discipline and exclusions

- The issuing board's public discipline, orders and actions for this person.
- Healthcare: HHS-OIG exclusions https://exclusions.oig.hhs.gov; DEA registration status where controlled-substance prescribing is part of the role https://www.deadiversion.usdoj.gov; board certification via ABMS https://www.abms.org for physicians.
- Securities and advisers: disclosure events on FINRA BrokerCheck https://brokercheck.finra.org and SEC IAPD https://adviserinfo.sec.gov, as the regulator publishes them.
- Mortgage: NMLS Consumer Access https://www.nmlsconsumeraccess.org regulatory actions.
- Attorneys: the state bar's public discipline record.
- Contractors: the contractor board's complaint and bond/insurance information where the board shows it; BBB https://www.bbb.org complaints about the business (a business record, not a personal one).

If an official regulator record shows a disclosure, report exactly what it says with the link and date, and recommend the user discuss it with the professional and with counsel. Do not dig further.

## Layer 3: Profession-specific checks

| Profession | Check |
| --- | --- |
| Physician / NP / PA | Scope of practice and any supervision or collaboration requirement in the user's state for the planned work; board certification if claimed |
| Nurse | License type matches the tasks (RN vs LPN vs APRN); multistate privilege where claimed, confirmed at the board |
| Pharmacist / pharmacy | Pharmacist and pharmacy licenses at the state board; for outsourcing facilities, FDA's registered list https://www.fda.gov/drugs/human-drug-compounding/registered-outsourcing-facilities |
| Attorney | Admitted in the right jurisdiction; good standing |
| CPA / financial | License or registration covers the service; regulator disclosures |
| Contractor | License class covers the job size and type; bond and insurance per the board; permits are the user's to pull or confirm |
| Engineer / architect | License in the project's state; firm registration if the state requires it |

## Layer 4: Professional reputation (optional, user-requested)

Only the professional's or business's own published professional work and public reviews of their professional services on the platforms the profession uses. Summarize themes; never quote reviewers' personal details. Skip personal social media.

## Layer 5: References

You do not contact references. Give the user a short list of job-related reference questions they can ask, and remind them that their own background-check or reference process should follow their counsel's advice.

## Red flags (report with source)

- License expired, suspended, revoked, surrendered, or restricted in a way that affects the planned work.
- Public board discipline or a regulator disclosure relevant to the role.
- OIG exclusion (healthcare).
- License type or class does not cover the planned work, or the license is in a different state.
- Name, license number or credential the person gave does not match the official record.
- Claimed certification that the certifying body does not show.

## Report

```markdown
# Credential report: [Name], [credential]  (prepared [YYYY-MM-DD])

Not a background check or consumer report. Public professional-license and regulator records only.

## Summary
[2–3 sentences]
**Assessment (for your review):** No concerns found in the sources checked / Follow up before proceeding ([reason]) / Serious concern ([reason, source])

## Licenses
| State | Type | Number | Status | Expires | Restrictions | Source + date |

## Regulator records
| Source | Result | Link | Date |

## Profession-specific checks
[findings]

## Red flags
[none found / list with sources]

## Not checked
[source, reason: e.g. CAPTCHA; user to complete]

## Suggested questions for the professional
[job-related questions the user can ask]

## Next steps
[e.g. confirm scope-of-practice question with the board; if a background check is needed, use an FCRA-compliant screening company with counsel]
```

The user makes the decision. If a background check is needed for a hiring decision, point the user to an FCRA-compliant background-screening company and their employment counsel; do not name or recommend a specific vendor.
