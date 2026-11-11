---
name: verify-license
description: Use when the user asks whether a professional is licensed, wants a license number checked, or needs license status, expiry and board discipline confirmed in any US state. Routes to the right state board or national registry, looks up one person at a human pace, and returns a dated, cited verification summary. Public license records only.
license: Apache-2.0
---

# Verify a license

**Load `professional-finder:ground-rules` first and follow it throughout.** Its hard rules, FCRA and anti-discrimination cautions and output conventions apply to every step below.

Confirm that a professional holds an active license for the work, in the state where the work happens, with the source and date recorded.

## Inputs

- Full name as licensed (ask for middle initial if the name is common).
- Profession and license type.
- State where the work will be done (and the state they say they are licensed in, if different).
- License number, NPI, CRD or NMLS number if the user has it (optional, speeds the lookup).

Never ask for a Social Security number (full or partial), date of birth or other personal identifiers. If a board's search form offers such fields, leave them blank.

## Routing

| Profession | Primary source | Also check |
| --- | --- | --- |
| Physician (MD/DO) | The state medical board's license search (state board method) | FSMB DocInfo https://www.docinfo.org for multi-state history; ABMS https://www.abms.org for board certification |
| Nurse (RN/LPN/APRN) | State board of nursing | Nursys https://www.nursys.com where the state participates; confirm at the state board |
| Any healthcare provider | State board for that profession | NPI Registry https://npiregistry.cms.hhs.gov (identity only, not a license); OIG exclusions https://exclusions.oig.hhs.gov; DEA https://www.deadiversion.usdoj.gov for controlled-substance prescribers |
| Attorney | State bar or state supreme court attorney search | Other states where they say they are admitted |
| CPA | State board of accountancy | Other states where they say they practice |
| Broker / registered rep | FINRA BrokerCheck https://brokercheck.finra.org | State securities regulator (NASAA https://www.nasaa.org lists them) |
| Investment adviser | SEC IAPD https://adviserinfo.sec.gov | State securities regulator |
| Insurance producer | State insurance department | NIPR https://www.nipr.com |
| Mortgage loan originator | NMLS Consumer Access https://www.nmlsconsumeraccess.org | State financial regulator |
| Real estate agent / broker | State real estate commission | |
| Appraiser | State appraiser board | ASC https://www.asc.gov |
| Contractor / trades | State contractor or trade board; city or county licensing office where trades are local | BBB https://www.bbb.org for complaints (not a license source) |
| Engineer / surveyor | State engineering board | NCEES https://ncees.org |
| Architect | State architecture board | NCARB https://www.ncarb.org |
| Teacher | State education department | |
| Anything else | State board method in `professional-finder:ground-rules` | Relevant certification body |

To find any state board, follow "How to find the right licensing board in any state" in `professional-finder:ground-rules`. Do not guess URLs.

## Lookup steps

1. Open the official source. If it shows a CAPTCHA, login or terms-of-use gate, stop and give the user the URL and the exact search to run.
2. Search by name (and number if supplied). If several people match, narrow by city, license type or number; if still ambiguous, report all plausible matches and ask the user to confirm with the professional.
3. Read the record: license type, number, status, original issue date, expiry date, any restrictions or conditions, and any public discipline or board orders.
4. Check that the license type covers the planned work and that the state matches where the work will happen.
5. For healthcare roles, run the OIG exclusion check as well.

## Status meanings (common terms; the board's own definitions control)

| Status | Meaning | What to tell the user |
| --- | --- | --- |
| Active / Current / Clear | Licensed and in good standing per the board | Proceed; note expiry date |
| Active with conditions / probation / restricted | Licensed with limits | Read the order; follow up before proceeding |
| Inactive / Lapsed / Expired | Not currently authorized | Cannot practice under this license until renewed |
| Suspended / Revoked / Surrendered | Not authorized | Serious concern; cite the order |
| Not found | No match in this source | Not proof of anything; recheck spelling, other states, and ask the professional for their number |

## Output

```markdown
## License verification: [Name]  (checked [YYYY-MM-DD])

| Field | Finding |
| --- | --- |
| Name as licensed | |
| License type / number | |
| State | |
| Status | |
| Issued / Expires | |
| Restrictions or conditions | None shown / [detail] |
| Public discipline | None shown / [detail + link] |
| Covers the planned work? | Yes / No / Unclear (why) |

**Assessment (for your review):** No concerns found in the sources checked / Follow up before proceeding ([reason]) / Serious concern ([reason, source])

**Sources checked:** [database name, URL, date] ...
**Not checked:** [source, reason]
**Next step:** [e.g. run screen-candidate; ask the professional for their license number]
```

A verification summary reflects the record on the date checked. It is not a background check and not a consumer report (see the FCRA caution in `professional-finder:ground-rules`).
