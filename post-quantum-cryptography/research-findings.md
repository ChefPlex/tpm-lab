# What the Research Says

**Status:** 🚧 Research, October 2026. Built on [sources.md](sources.md); every fact here has a dated source there. Labels: **fact** is in a primary source; **inference** is my reading of the facts; **recommendation** is what I would do.

## The short version

**Confidentiality can move now. Authentication cannot, yet.** Hybrid post-quantum key exchange for TLS 1.3 is a published standard, and the major browsers, OpenSSL, Go and AWS already use it by default (fact). Post-quantum certificates for TLS server authentication are still drafts, and the browsers' own roadmap has no dates (fact). So the program runs as two tracks with two definitions of done: move confidentiality where the products are ready, and get the certificate, signing and identity estate ready for a change the ecosystem has not finished (recommendation).

**This is an inventory program before it is a cryptography program.** The algorithm swap is the easy part where a library or proxy does it. The hard part is the same as every encryption program: finding what is in use, on which hop, owned by whom, and proving it changed (inference, from the encryption programs linked below).

## What is ready, and for what

| Readiness | What falls here | Why |
|:---|:---|:---|
| **Ready for a lab prototype** | Hybrid TLS with OpenSSL 3.5 or Go 1.24; Envoy built from `main`; Istio's experimental `pqc` policy; ML-DSA keys in AWS KMS; a CBOM from source scanning | All available today; nothing here needs a production change |
| **Ready for a bounded production pilot** | Hybrid TLS on calls to AWS KMS and Secrets Manager; edge TLS where clients already offer X25519MLKEM768; services on Go 1.24 or Kubernetes 1.33 | Standard published, supplier support generally available, and the negotiated group can be observed (CloudTrail, Envoy 1.39 logging) |
| **Vendor-conditional** | Envoy's default (ships in 1.40, not yet released); Google Cloud KMS ML-KEM (Preview, with a conflicting blog); HSM fleets other than a validated line; Google load balancer default (planned October 2026) | The standard is ready; the specific product or version is not, or is not proven |
| **Standards-conditional** | TLS server authentication with ML-DSA; Merkle Tree Certificates; composite certificates; ML-KEM in IKEv2; PQ KEMs in JOSE/COSE | Approved or in drafting, not yet published |
| **Not mature** | Public web PKI with post-quantum certificates; Sigstore public signing; FN-DSA and HQC (no draft standards yet) | No date anyone can plan against |
| **Needs the company's own data** | Which data must stay confidential for 10+ years; which services have no owner; which HSMs, CAs and appliances are in the fleet; which customers pin certificates or run old clients | Only discovery answers these |

## The threat model, kept apart on purpose

Three different risks hide behind "quantum risk". They have different deadlines and different fixes, and one blended score would hide that.

| Risk | What an attacker does | When it matters | What fixes it | Track |
|:---|:---|:---|:---|:---|
| **Harvest now, decrypt later** | Records encrypted traffic today; decrypts it once a large enough quantum computer exists | **Today**, for any data that must stay secret longer than the time to such a machine | Post-quantum or hybrid key establishment on **every** hop the data crosses | A |
| **Future impersonation** | Forges a certificate or signature to pose as a server or service | Only once such a machine exists; it cannot be done retroactively to a past session | Post-quantum authentication: certificates, PKI, relying parties | B |
| **Long-lived signed evidence** | Forges a signature on old software, firmware or documents that are still trusted years later | For anything verified long after it was signed: firmware, release artifacts, roots of trust | Post-quantum or hash-based signing, timestamps, a plan for verifying old signatures | B |

**Forward secrecy does not help here** (inference). Ephemeral elliptic-curve keys protect past sessions against a stolen server key. They do not protect a recorded session against an attacker who can break the elliptic-curve exchange itself, which is exactly what a large quantum computer would do.

**Symmetric encryption is not the problem.** AES-256 stays (fact: NSA's CNSA 2.0 suite keeps AES-256 for all classification levels). The work is the public-key cryptography that protects the keys: key exchange, key wrapping and signatures. "Re-encrypt every database" is the wrong program.

### A planning rule, not a forecast

The usual heuristic is: if **how long the data must stay secret** plus **how long the migration takes** is longer than **the time until a quantum computer can break today's keys**, the data is already exposed. Nobody knows the last number, so the rule cannot produce a date. What it does is rank work:

| Data must stay confidential for | Migration takes | Reading |
|:---|:---|:---|
| 1 year | 3 years | Low priority for harvest-now risk; migrate with the platform |
| 5 years | 3 years | Exposed if the machine arrives within about 8 years; early cohort |
| 10 years | 4 years | Treat as exposed now; first cohort |
| 20+ years, or a root of trust | 5+ years | Treat as exposed now, and plan the signature track for it too |

These rows are **synthetic examples** for ranking, not a probability.

## Every hop counts

A customer request may cross public TLS to the edge, then internal TLS or mTLS to a gateway, then the mesh, then a database, then replication to another region and a backup. **Hybrid key exchange on the first hop and classical on the second leaves the data exposed** (inference). The unit of measurement is the data path, not the server. This is the same lesson as end-to-end encryption coverage in transit, one level deeper.

And **"capable" is not "used"**. A server that supports X25519MLKEM768 protects nothing if no client negotiates it. Credit goes to observed negotiated groups, which the major platforms now let you see (fact: CloudTrail `tlsDetails`, Envoy's `%DOWNSTREAM_TLS_GROUP%`).

## Where the encryption-program lessons land

This plan builds on two pieces about running encryption at scale: the [Encryption Program Playbook](https://github.com/ChefPlex/security-program-playbooks/blob/main/encryption-program-playbook.md) and [Lessons from Leading Large-Scale Encryption Programs](https://github.com/ChefPlex/learning-notes/blob/main/lessons-from-large-scale-encryption-programs.md). Each lesson needs a mechanism, not a slogan:

| Lesson | Where it lives in this program | How it fails if ignored |
|:---|:---|:---|
| Two unknowns: what is in use, and what is needed | Discovery workstream plus a separate scope decision by the sponsor | Coverage climbs while the scope quietly shrinks |
| Guard the denominator | Versioned scope register; every exclusion has an approver | "92 percent" that means 92 percent of what was left after removing the hard parts |
| Ownership is a workstream | Ownerless-service list from week 3; management assigns owners before remediation | Twenty orphaned central services take longer than two hundred owned ones |
| Coverage is a project, currency is permanent | Track A is coverage; crypto agility is the permanent capability | The company runs this program again for the next algorithm |
| The binding constraint is people | Capacity model naming the PKI, HSM and mesh teams | Thirty "parallel" work packages queued behind five engineers |
| Central builds the path, teams adopt it | Mesh, gateways, shared libraries and managed KMS carry most of Track A | A hundred teams each choose a slightly different construction |
| Priority is displacement | A written agreement per team on what moves out | Executive agreement that never reaches a sprint |
| Plan to be blocked | Re-solve time in the schedule; two-day escalation | The first failed approach is defended for a quarter |
| Measure with a script | Negotiated-group telemetry and CBOM scans, not surveys | A dashboard of what teams believe |
| End at diminishing returns, in the open | Time-limited exceptions; scope reduction agreed by the sponsor | A program that cannot stop, or stops and calls it failure |

## What an earlier draft got wrong

This research started from an AI-written strategy draft. Checking it against primary sources changed several facts, which is the reason sources come first:

- **The NIST timeline is still a draft,** and its "deprecated after 2030" applies only to 112-bit strength keys. Everything is "disallowed after 2035".
- **RFC 9954 is the TLS hybrid design document,** not a general framework for combining key mechanisms.
- **ML-DSA for signed tokens (JOSE/COSE) is already an RFC** (9964, May 2026), not "still a draft".
- **Google Cloud KMS ML-KEM is Preview** in the release notes, despite a blog post calling it generally available. The signature algorithms are generally available.
- **No OpenSSL post-quantum provider is FIPS-validated yet;** one HSM line is.
- **Envoy's post-quantum default is merged but not released.**
- **NIST did not state that HAWK's vulnerability left ML-KEM and ML-DSA unaffected.** That statement came from the researchers who found it.
- **The draft missed the item with the most direct effect on a vendor:** an executive order directing a federal acquisition rule for contractors, with a 2030 deadline.
