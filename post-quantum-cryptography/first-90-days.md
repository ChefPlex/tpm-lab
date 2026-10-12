# The First 90 Days

**Status:** 🚧 Draft, October 2026. Weeks 1 to 4 are written out in full; weeks 5 to 13 are an outline to be filled in as the research and the charter settle.

The enterprise is fictional: **Meridian Cloud Systems**, a global multi-tenant SaaS company on two public clouds, with a few hundred services, more than 100 engineering teams, a service mesh, cloud key management, HSM-backed root keys and its own private certificate authorities. Every name, number and decision in this file is a **synthetic example**. Where a decision is marked "simulated", nobody approved anything; the file shows what the decision would need.

## The point of the first 90 days

**Day 90 is not a slide deck. It is a working program**: a baseline that says how big the problem is, a pilot that proves one path works, owners for the work, and a plan leadership can fund with its eyes open.

Three rules carry the whole quarter, and each comes from a program that has been run before ([Encryption Program Playbook](https://github.com/ChefPlex/security-program-playbooks/blob/main/encryption-program-playbook.md)):

1. **Baseline before you promise.** Two unknowns, and they are different problems: what cryptography is in use today, and what each service actually needs. The first is found by looking. The second is decided, by someone with the authority to decide. No completion date is committed until both are known well enough to size.
2. **Ownership is a workstream.** Finding the services is easy. Finding who can change them is the work, and the services with no team left are usually the old, central, high-risk ones.
3. **Plan to be blocked.** Some paths that look fine on paper will not work. The loop back to the architects is in the schedule from week 1, not added when the first one fails.

## Who is in the room

Roles, not people. One person can hold more than one role in a smaller company.

| Role | What they own in the first 90 days |
|:---|:---|
| Executive sponsor (CISO) | The case for action, funding, the trade-offs only an executive can make |
| Co-sponsor (VP Platform Engineering) | Platform team capacity, the paved-road commitment |
| Lead TPM | The program: plan, cadence, decisions, dependencies, escalation, reporting |
| Chief cryptography architect | Approved algorithms and profiles, the reference architecture, technical decisions |
| PKI and HSM operations lead | Certificate authorities, key ceremonies, HSM capability, recovery |
| Network and mesh lead | Edge TLS, service mesh, the hop-by-hop picture |
| Cloud platform lead | What the cloud providers support, by service, region and version |
| SRE lead | Pilot safety, change gates, rollback |
| GRC lead | Which rules apply, risk acceptance, evidence |
| Data and metrics engineer | Inventory model, discovery automation, the dashboard |

## Weeks 1 to 4: understand and organize

### Week 1: Sponsor, scope question, and the first map

- **Objective:** agree why the program exists, who decides what, and what we already know.
- **Meetings:** sponsor kickoff (60 min); architecture lead working session (90 min).
- **Tasks:**
  - Write the one-page case for action: harvest now, decrypt later for long-lived data; the standards that now exist; why waiting raises the cost.
  - Draft decision rights: who approves an algorithm profile, a scope change, a risk exception, a production rollout.
  - Collect what already exists: service catalog, CMDB export, certificate authority inventory, HSM and KMS inventory, mesh configuration, prior TLS and encryption program records.
  - Start the standards baseline from [sources.md](sources.md): what is final, what is draft, what applies to us.
- **Outputs:** case-for-action draft; decision-rights table; list of existing evidence sources with an owner for each.
- **Done when:** the sponsor has read the case for action and named a co-sponsor in platform engineering.
- **Decision needed:** program sponsor and co-sponsor confirmed (simulated).
- **Blocker trigger:** no platform co-sponsor by Friday. Escalate to the CISO: without platform ownership there is no paved road and the program becomes 100 separate migrations.

### Week 2: The vocabulary and the inventory model

- **Objective:** one language for the program, and a data model the inventory can grow into.
- **Meetings:** architecture working session; GRC working session (60 min).
- **Tasks:**
  - Write the cryptographic function taxonomy. These have **separate definitions of done**: key establishment in transit, authentication and signatures, key wrapping for data at rest, software and firmware signing, and the currency of the policy itself.
  - Draft the inventory data model: services, assets, data flows, hops, observed cryptography, keys and certificates, owners, exceptions, scope changes.
  - Define the evidence states: unassessed, classical, PQC-capable, PQC observed, verified end to end. "Capable" is not "used".
  - Draw the first trust-boundary picture for one high-value data path, every hop from customer to storage.
- **Outputs:** taxonomy; inventory schema v0; evidence-state definitions; one data-path diagram.
- **Done when:** the architect and the GRC lead agree the taxonomy, in writing.
- **Decision needed:** what counts as "in scope" for the first baseline (simulated).
- **Blocker trigger:** disagreement on whether signatures are in the first phase. Bring it to the sponsor as an explicit trade-off, not a debate.

### Week 3: Discovery sources and the paved-road question

- **Objective:** know where the evidence will come from, and which work can be done centrally.
- **Meetings:** platform leads (mesh, PKI, KMS, developer platform) joint session (90 min); first vendor triage.
- **Tasks:**
  - List discovery sources and what each can see: TLS handshake telemetry and negotiated groups, mesh policy, code and dependency scanning, certificate authority records, HSM and KMS metadata, signing pipelines, network appliances. No single source is complete.
  - Split the work: what a central change covers (mesh, gateways, shared libraries, managed KMS) and what needs each application team.
  - Start the supplier matrix: product, version, PQC status (announced, preview, generally available), function covered, FIPS context, evidence link.
  - Start the risk register and the ownership-gap list.
- **Outputs:** discovery plan with an owner per source; central-versus-application split, first cut; supplier matrix v0; risk register v0.
- **Done when:** every discovery source has a named owner and a first pull date.
- **Decision needed:** none. Flag early if the mesh or gateway owner cannot commit capacity.
- **Blocker trigger:** a discovery source has no owner after two working days. Escalate to the TPM, who names a decision owner the same day.

### Week 4: Charter draft and pilot candidates

- **Objective:** a charter that can be reviewed, and a short list of places to prove the approach.
- **Meetings:** charter review with sponsors (60 min); pilot selection with architecture and SRE.
- **Tasks:**
  - Draft the charter from [charter.md](charter.md): outcomes by cryptographic function, scope and out of scope, decision rights, guardrails, funding approach.
  - Size the unknowns honestly: how much of the estate is unassessed, how many services have no confirmed owner.
  - Pick two or three pilot candidates: one internal mesh path with low blast radius, one external API path with long-lived sensitive data, one KMS or secrets API call.
  - Open the decision log.
- **Outputs:** charter draft; pilot shortlist with the reason for each; unknowns sized as ranges; decision log.
- **Done when:** sponsors have reviewed the charter draft and the pilot shortlist.
- **Decision needed:** approve the charter draft for the day-30 gate (simulated).
- **Blocker trigger:** nobody will own a pilot. That is a capacity signal, not a scheduling one. Take it to the sponsor as a trade.

### Day-30 gate

Review-ready charter, initial threat and risk model, discovery plan with owners, ownership model, operating cadence, pilot shortlist. **Report what is unknown as plainly as what is known.** If the sign-off is simulated, the gate record says so.

## Weeks 5 to 13: outline

| Week | Focus | Main output |
|:---|:---|:---|
| 5 | Architecture options and decision records | ADRs: hybrid TLS profile; central mesh adoption; separate signature track |
| 6 | Hybrid TLS test design | Lab test specification: advertised versus negotiated group, failure and fallback cases |
| 7 | PKI, HSM and signing | Capability check per HSM and CA; ceremony and recovery requirements; rollback design |
| 8 | Lab rehearsal | Pilot results where actually run, or a test specification marked "not run" |
| **Day-60 gate** | | Reference architecture, draft profiles, pilot plan, dependency and capacity model v1 |
| 9 | Workstreams and owners | Workstream charters with an engineering owner and a TPM each; the ownerless-service plan |
| 10 | Capacity and money | Bottleneck model; base, accelerated and constrained scenarios; the priority-displacement agreement |
| 11 | Rollout safety | Pilot rollout and rollback protocol; exception workflow; supplier escalation |
| 12 | Measurement | Scorecard, denominator policy, executive readout draft |
| 13 | Steering checkpoint | Decision package: scope, policy, funding, pilot authority, next 2 to 4 quarters (simulated) |
| **Day-90 gate** | | 12 to 18 month plan, multiyear milestones, dependency map, capacity and budget assumptions, risk baseline, decision package |

## What usually goes wrong in the first 90 days

- **Remediating what you already know about.** It feels like progress and moves no real number while the denominator is still growing.
- **A dependency chart that hides the queue.** Thirty work packages that all need the same five-person PKI and HSM team are not parallel. Model that team by name with its capacity in week 10, and earlier if it shows up.
- **Priority agreed at the top that never reaches a sprint.** Executive agreement does not enter an engineering team's plan by itself. Week 10's displacement agreement names the work that moves out, team by team.
- **Calling hybrid key exchange "done".** It protects confidentiality on that hop. It does not change the certificate that authenticates the server, or any other hop on the path.
