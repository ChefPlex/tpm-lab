# Program Charter: Quantum Shield

**Status:** 🚧 First draft, October 2026. Nothing here is approved; every approval is simulated. Targets are proposals until the day-90 baseline exists.

**The enterprise is fictional:** Meridian Cloud Systems, a global multi-tenant SaaS company. Its architecture, numbers and people are **synthetic examples**, not a description of any real company.

---

## The one-page version

**The problem.** Meridian protects customer data, service identities and software with public-key cryptography (RSA and elliptic curves) that a large enough quantum computer could break. Nobody can say when such a machine will exist. Traffic recorded today can be decrypted later, so data that must stay confidential for ten years is already exposed if it crosses a network today under classical key exchange. Signatures and certificates carry a different risk: forgery in the future, which matters most for long-lived roots of trust and signed software.

**Why now.** Final standards exist for the replacement algorithms, and the major libraries, browsers and cloud providers have started shipping them (status and dates in [sources.md](sources.md)). A company-wide migration at this scale takes years. Starting late means migrating under deadline pressure.

**What we will do.** Find where quantum-vulnerable cryptography is used and who owns it. Move the highest-risk confidentiality paths to hybrid post-quantum key establishment first, through central platforms (mesh, gateways, shared libraries, managed key services) rather than 100 separate team projects. Run signatures, certificates and identity as a separate track, because that ecosystem is less mature. Build the ability to change algorithms again without another multiyear program.

**What we will not claim.** That Meridian is "quantum safe". That enabling a capable library means it is used. That hybrid key exchange fixes authentication. That every database needs re-encrypting: symmetric encryption such as AES-256 is not the problem.

**The ask for the first 90 days.** A small core team, named owners in platform engineering, access to the inventories that already exist, and a decision at day 90 on funding the plan the baseline supports.

---

## 1. Outcomes, by cryptographic function

Each function has its own definition of done. One blended percentage would hide the gap between them.

| Function | Outcome we want | How we will know | Target status |
|:---|:---|:---|:---|
| Key establishment in transit | Highest-risk data paths use hybrid post-quantum key exchange on **every** hop | Observed negotiated groups per hop, not configuration | Proposed |
| Keys protecting data at rest | Asymmetric key wrapping and key exchange around stored data identified and on a migration path | Key-management inventory and design review | Proposed |
| Authentication and certificates | Private PKI able to issue post-quantum or hybrid certificates; relying parties tested | Lab and pilot evidence per CA and relying party | Proposed, maturity-dependent |
| Software and firmware signing | Long-lived signing roots and release signing on a migration plan; old signatures still verifiable | Signing inventory, verifier support, timestamp strategy | Proposed, maturity-dependent |
| Crypto agility | An algorithm change can roll across an important service group in weeks, not years | Measured change lead time on a rehearsal | Proposed |
| Visibility | A cryptographic inventory that is mostly observed, not self-reported, with owners | Share of inventory backed by automated evidence | Proposed |

## 2. Scope

**In scope:** public edge and API TLS; service mesh and internal mTLS; cloud key management and secrets APIs; HSMs and key ceremonies; private certificate authorities; identity tokens and federation where Meridian signs; software release signing; VPN, SSH and network appliances; customer-facing SDKs and integrations as a compatibility workstream; the inventory, policy and exception process.

**Out of scope:** quantum key distribution; quantum hardware research; replacing AES everywhere; writing cryptography from scratch; public web PKI decisions that belong to browsers and certificate authorities (we follow them, we do not set them); claims about any real company's readiness.

**Controllable versus conditional.** Meridian controls its own platforms, policies, inventory and rollout. It does not control standards bodies, browser release schedules, customers' software, or a vendor's firmware roadmap. Every milestone that depends on one of those is marked conditional, with the dependency named.

## 3. Guardrails

- **Reliability first.** No change goes past canary without SRE sign-off and a tested rollback.
- **A rollback is a security decision too.** Reverting to classical-only restores availability and also restores the exposure. Every revert opens a time-limited exception with an owner and a date.
- **The denominator is versioned.** Coverage never improves by quietly removing hard work from scope. Every scope change is logged with who approved it and why.
- **Evidence over assertion.** "PQC-capable" is not "PQC in use". Credit goes to observed behavior.
- **Approved implementations only.** Standard, maintained libraries and validated modules where required. No custom constructions.

## 4. Governance and decision rights

| Decision | Decides | Consulted | Informed |
|:---|:---|:---|:---|
| Approved algorithms and profiles | Cryptographic Architecture Review Board | Platform leads, GRC | All engineering |
| Scope and denominator changes | Executive sponsor | Lead TPM, GRC, architect | Steering committee |
| Risk exceptions (high risk) | Executive sponsor | Architect, GRC, service owner | Steering committee |
| Risk exceptions (standard) | Architecture Review Board | GRC, service owner | Lead TPM |
| Production canary promotion | SRE lead with the workstream owner | Architect, Lead TPM | Steering committee |
| Rollback | SRE on-call (immediately) | Workstream owner | Exception opened within 1 working day |
| Root CA or trust-anchor change | Architect with the PKI and HSM lead | GRC, SRE | Steering committee |
| Service ownership assignment | Engineering VP for that area | Lead TPM | Program team |
| Program closure | Executive sponsor | Steering committee | All |

**Cadence.** Weekly program execution review (blockers, dependencies, decisions due). Biweekly architecture and exception forum. Monthly supplier and compliance review. Monthly executive review (exposure reduced, what is stuck, decisions needed). Quarterly steering and rebaseline.

**Escalation.** Anything blocked for two working days goes to the TPM, who names a next action and a decision owner. Surfacing a blocker is never held against the team that raised it.

## 5. Workstreams

Each has an engineering owner and a TPM counterpart. Detail lands in the next iteration.

1. Discovery, inventory and ownership
2. Standards, profiles and architecture
3. Edge and API TLS, including client compatibility
4. Service mesh and internal mTLS
5. Cloud key management and secrets
6. HSM, key ceremonies and private PKI
7. Identity, federation and signing (the separate maturity-dependent track)
8. Network appliances, VPN and SSH
9. Customer and partner integration
10. Policy, exceptions, evidence and supplier readiness

**Two tracks, reported separately.** Track A is confidentiality: deploy where the standards and products are ready now. Track B is authenticity: certificates, signatures and identity, engineered for readiness while the ecosystem matures. Track B does not block Track A.

## 6. Milestones and stage gates

| Gate | When (proposed) | What must be true |
|:---|:---|:---|
| Day 30 | Week 4 | Review-ready charter, discovery plan with owners, pilot shortlist |
| Day 60 | Week 8 | Reference architecture, draft profiles, pilot plan or lab results, capacity model v1 |
| Day 90 | Week 13 | Baseline with confidence ranges, 12 to 18 month plan, funding decision package |
| Pilot in production | After day 90 | Gate A to C passed for one internal and one external path |
| Track A scale-out | Year 1 to 2 | Highest-risk paths covered on every hop, with observed evidence |
| Track B readiness | Maturity-dependent | Private PKI and signing ready for relying-party migration |

Detail: [first-90-days.md](first-90-days.md).

## 7. Capacity, funding and contingency

- **Fund in stages.** Discovery and mobilization first. The bottom-up cost model comes after the baseline, not before.
- **Model the scarce teams by name.** PKI, HSM, mesh and SRE capacity usually sets the schedule, not the dependency graph.
- **Contingency is explicit.** Build in 10 to 20 percent and say so, with the assumptions behind it.
- **Adding people does not always shorten the schedule.** If the five-person PKI team is the queue, more application engineers change nothing.

## 8. Definition of success

- **Success:** highest-risk confidentiality paths covered on every hop with observed evidence; signing and PKI on an agreed, funded path; an inventory that stays current without a program to run it; a rehearsed algorithm change.
- **Partial success, stated honestly:** a long tail of legacy systems with documented exceptions, owners and expiry dates, scoped out in the open and agreed by the sponsor.
- **Closure:** when the work no longer needs coordinating, not when a number hits 100. Crypto policy, inventory, supplier tracking and exceptions move to a named permanent owner.

## 9. Open items before approval

Tracked in [open-questions.md](open-questions.md). The ones that affect this charter most:

- **Which rules bind Meridian, and how.** Today only US federal agencies and national security systems are legally required to migrate. A planned federal acquisition rule would extend a 2030 deadline to covered contractors, and FedRAMP providers are already being asked about it ([sources.md](sources.md) §3). If Meridian sells to the US government, its deadlines are set there, not by this charter.
- **What HSM and CA vendors can actually deliver, and when.** One HSM line has a validated module with the new algorithms; most do not yet.
- **How much of the estate is unassessed,** and how many services have no owner.

## 10. Approval (simulated)

| Role | Decision | Date |
|:---|:---|:---|
| Executive sponsor (CISO) | Not yet reviewed | |
| Co-sponsor (VP Platform Engineering) | Not yet reviewed | |
| Chief cryptography architect | Not yet reviewed | |
| GRC lead | Not yet reviewed | |
