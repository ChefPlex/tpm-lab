# Risk Tiers and Risk Register

**Status:** 🚧 First draft, November 2026. Built on [research-findings.md](research-findings.md) and [sources.md](sources.md); every fact here traces to a dated row there. Labels: **fact**, **inference**, **recommendation**, as in the research. Every example is **synthetic** and belongs to the fictional Meridian Cloud Systems.

## Why this file exists

The program ranks work by risk, and "risk" means two different things here. Keep them apart, with different owners and different registers:

| Register | Question it answers | Unit | Owner |
|:---|:---|:---|:---|
| **Exposure** | What could an attacker do to this data or this trust anchor, and how soon does it matter? | A data path or a key | The service or platform owner |
| **Delivery** | What could stop the program from finishing on time, or make it report progress it did not make? | A program risk | The lead TPM, with a named owner per row |

One blended score would hide which threat drives a row and whether the fix is ours to make (inference, from the threat model in the research).

## Part 1: Exposure tiers

### What is recorded for each data path

| Input | Values | Where it comes from |
|:---|:---|:---|
| Threat | Harvest now, decrypt later · Future impersonation · Long-lived signed evidence | [Threat model](research-findings.md#the-threat-model-kept-apart-on-purpose) |
| Confidentiality lifetime | Years the data must stay secret | Data owner, from retention and contract terms |
| Worst network zone crossed | Internal · Partner or supplier · Internet · Customer network | [Backlog item 0](backlog.md) |
| Function | Key establishment · Certificate or signature · Root of trust or long-lived signing key | Discovery (item 1a) |
| External obligation | None · Regulated customer questionnaire · FedRAMP · Federal contract · National security system | [Sources §3](sources.md#3-government-and-regulation) |
| Fix readiness | The six readiness bands, from "ready for a pilot" to "needs our own data" | [Research](research-findings.md#what-is-ready-and-for-what) |
| Evidence state | Observed · Self-reported · Unknown | Discovery (item 1a) |

### The tiers

A decision table, not a weighted score. Take the **highest** tier any rule assigns.

| Tier | Assign it when | What it means |
|:---|:---|:---|
| **T1, exposed now** | Harvest-now data that must stay secret **10+ years** · any **root of trust or long-lived signing key** · any path with a **dated external obligation** | First cohort. Plan both tracks now. |
| **T2, early cohort** | Harvest-now data with a **5 to 10 year** lifetime · any path that crosses a zone we do not control at both ends and carries customer data · **evidence state unknown** | Second cohort. Unknown is never treated as low. |
| **T3, move with the platform** | Lifetime **under 5 years**, internal zone only | Moves when the central platform default changes; no team project. |
| **T4, monitor** | No quantum-vulnerable public-key cryptography found (observed, not self-reported) | Recheck at each quarterly rebaseline. |

The lifetime cut-offs follow the planning rule in the research: lifetime plus migration time compared with an unknown arrival date. **They rank work; they do not predict a date** (inference).

**Three rules that keep the tiers honest:**

1. **A path takes the tier of the most sensitive data that crosses it, and every hop on it inherits that tier.** One protected hop does not protect the path (inference, from "every hop counts").
2. **Readiness changes the action, never the tier.** A T1 path whose fix is standards-conditional still sits in T1. It gets a time-limited exception, a compensating control and a named trigger ("re-plan when the ML-DSA-in-TLS document is published"), never a quiet "wait".
3. **Credit is for what is negotiated, not what is supported.** A path moves down only on observed evidence (negotiated groups in logs, a CBOM scan), never on a survey answer (inference, from "capable is not used").

### Symmetric ciphers and hashing

These are in scope for the **inventory**, and they are a review, not a migration. AES-256 stays: NSA's CNSA 2.0 keeps it for all classification levels (fact). Shorter symmetric keys and hash sizes are listed and checked against the approved profile (recommendation). The exact CNSA 2.0 hash requirements were **not checked** in this research.

### How the tier drives the program

| Tier | Sequence | Exception approver (from the [charter](charter.md)) | Longest exception (recommendation) | Reported to executives |
|:---|:---|:---|:---|:---|
| T1 | Cohort 1 | Executive sponsor (high risk) | 6 months, renewable once with a named trigger | Every path, every month |
| T2 | Cohort 2 | Architecture Review Board | 12 months | Count and trend |
| T3 | Platform default | Architecture Review Board | Until the platform default ships | Count only |
| T4 | None | None | None | Not reported |

## Part 2: The register format

Both registers use the same columns, so one dashboard can read them.

| Column | Rule |
|:---|:---|
| ID | Never reused. A closed row stays in the log. |
| Type | Exposure or Delivery |
| Statement | **Cause, event, effect** in one sentence: "Because X, Y may happen, which would cause Z." |
| Tier or severity | Exposure rows: T1 to T4. Delivery rows: high, medium, low. |
| Likelihood driver | What would make it more likely. A date, a vendor, a standard, a team. |
| Owner | **One person**, not a team. |
| Response | Avoid · Mitigate · Transfer · Accept |
| Trigger | The observable event that re-rates the row. **A risk with no trigger is a worry, not a managed risk.** |
| Conditional on | The vendor, standard or regulator the fix waits for, if any |
| Status | 🟢 / 🟡 / 🔴 |
| Evidence and date | A link, and the date it was last true |

**Two operating rules.** An accepted risk carries an expiry date, like an exception. **A row should never jump from 🟢 to 🔴.** A managed risk shows 🟡 first; a jump means it was not being watched, or something outside scope happened, and either one is a finding for the next review.

## Part 3: Delivery register, version 0

Seeded from the research. The causes are facts from [sources.md](sources.md) as of October 2026; the effects and responses are this plan's.

| ID | Statement | Severity | Response | Trigger | Conditional on |
|:---|:---|:---|:---|:---|:---|
| D1 | Because most HSM lines are not yet validated for the new algorithms (one is), signing and key work may wait on firmware, which would push Track B and any T1 signing key | High | Mitigate: supplier matrix, a validated line for new keys, plan for both upgrade and replace | A supplier's validation certificate lists ML-KEM or ML-DSA | HSM suppliers |
| D2 | Because post-quantum TLS server authentication is not yet published and the browser roadmap has no dates, Track B cannot finish on a fixed date | High | Accept, with Track B reported separately so it never blocks Track A | The ML-DSA-in-TLS document is published as an RFC | IETF, browsers |
| D3 | Because hybrid key shares are larger (an X25519MLKEM768 client share is 1,216 bytes, over QUIC's 1,200-byte first datagram), some middleboxes may fail, which would cause outages during rollout | Medium | Mitigate: lab test plan (backlog item 6), canary, rollback that opens an exception automatically | A failed canary, or a supplier advisory | Network appliance suppliers |
| D4 | Because hard paths are easy to drop from scope, coverage may climb while the scope shrinks, which would report progress that did not happen | High | Avoid: versioned denominator; every exclusion approved by the sponsor | Any scope change | None |
| D5 | Because some services have no owner, their migration may wait indefinitely, which would leave a long T1 or T2 tail | High | Mitigate: owner assigned by the engineering VP before remediation starts | Ownerless list not shrinking for two reviews | None |
| D6 | Because PKI, HSM and mesh teams are few, work packages may queue behind them, which would make "parallel" plans serial | High | Mitigate: capacity model naming those teams (backlog item 5) | Their queue exceeds one quarter | None |
| D7 | Because customers and partners run their own clients and may pin certificates, a path into the customer network may not move end to end | Medium | Transfer or accept: fallback and exception policy, supplier and partner questionnaire (backlog item 10) | A partner's roadmap date, or its absence | Partners, customers |
| D8 | Because servers can advertise support that clients never negotiate, the dashboard may count capability as protection | Medium | Avoid: count only observed negotiated groups | Telemetry missing for any T1 path | None |
| D9 | Because the US contractor rule is not yet proposed and NIST's transition timeline is still a draft, external dates may move | Medium | Accept: monthly recheck (dated rechecks in [open-questions.md](open-questions.md)) | The FAR proposed rule, or a final IR 8547 | Regulators, NIST |
| D10 | Because some product defaults are announced but not released (Envoy 1.40) or in conflicting status (Google Cloud KMS ML-KEM), a plan built on them may slip | Medium | Mitigate: plan only against released, generally available versions | Release notes | Suppliers |
| D11 | Because the algorithm set is still changing (a signature candidate withdrawn in July 2026, the backup KEM still without a draft), the company may need to change algorithms again | Medium | Mitigate: crypto agility as the permanent result, not a one-time swap | A NIST selection or withdrawal | NIST |

## Part 4: Exposure register, synthetic examples

| ID | Path or asset | Threat | Lifetime | Worst zone | Tier | Readiness | Owner | Status |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| E1 | Customer API, edge to mesh to database to cross-region backup | Harvest now | 10+ years (contract retention) | Internet | T1 | Edge ready for a pilot; backup replication needs our own data | Platform edge lead | 🟡 edge hop observed hybrid; backup hop unknown |
| E2 | Release signing root | Long-lived signed evidence | n/a (verified for years after signing) | Internal | T1 | Vendor-conditional (HSM) | PKI and HSM lead | 🟡 exception open, trigger D1 |
| E3 | Internal metrics batch job | Harvest now | Under 1 year | Internal | T3 | Moves with the mesh default | Mesh platform lead | 🟢 |
| E4 | Partner settlement file transfer | Harvest now | 7 years | Partner | T2 | Needs the partner's roadmap | Partner integrations lead | 🟡 questionnaire sent, no date returned |

## What the monthly executive review sees

- T1 paths: total against the versioned denominator, how many are **observed** protected on every hop, and exceptions open and expiring this month.
- Delivery risks at 🟡 or 🔴, each with the decision or help needed.
- Conditionals: which suppliers, standards or regulators the plan is waiting on, and whether any trigger fired.
- Unknowns: how many paths still have no evidence state. This number should fall every month.
