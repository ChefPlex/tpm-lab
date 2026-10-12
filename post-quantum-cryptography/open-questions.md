# Open Questions

**Status:** 🚧 Live register, October 2026. Questions the research could not settle, and what would settle each one. Questions about the fictional company are answered by assumption in later work and labelled synthetic.

## Standards and products to recheck

| # | Question | Why it matters | What settles it | Recheck |
|:---|:---|:---|:---|:---|
| S1 | Is NIST IR 8547 still a draft, and are its 2030 and 2035 dates unchanged? | The only NIST timeline; programs quote it as final | CSRC page for IR 8547 | Quarterly |
| S2 | Has the FAR proposed rule from EO 14412 been published, and how does it define "covered contractor"? | Turns guidance into a contract requirement for vendors to federal agencies by 2030-12-31 | Federal Register search | Monthly; due about 2026-12-19 |
| S3 | When do draft-ietf-tls-mldsa and draft-ietf-tls-mlkem publish as RFCs? | Starts the clock on TLS authentication planning | RFC Editor queue | Monthly |
| S4 | When do Merkle Tree Certificates leave working-group draft, and do browsers put dates on their roadmap? | Public web authentication cannot move before this | IETF datatracker; Chromium roadmap page | Quarterly |
| S5 | Is Google Cloud KMS ML-KEM generally available or still Preview? | The release notes and a product blog disagree | Release notes entry for KEMs | At next check |
| S6 | When does Envoy 1.40 ship with the post-quantum default? | Moves the mesh path from "build from main" to "upgrade" | Envoy release notes | At release |
| S7 | Which HSM lines have a CMVP certificate listing ML-KEM and ML-DSA? | Only one line is validated today; root keys live in HSMs | CMVP search, vendor by vendor | Quarterly |
| S8 | When does a validated OpenSSL provider include ML-KEM and ML-DSA? | Many FIPS-scoped services run on it | CMVP modules-in-process list | Quarterly |
| S9 | Are FN-DSA (FIPS 206) and HQC drafts published? | Smaller signatures; a backup KEM | CSRC FIPS list | Quarterly |
| S10 | What did the 2022 CNSA 2.0 per-category timeline say, and is it still current? | Some vendors still quote 2033 dates from it | The archived NSA advisory | Once |
| S11 | What does OMB M-26-15 mean by "Symmetric-key-based protocols should also be avoided" (Appendix A)? | It contradicts the memo's own algorithm list and NSA's guidance | Quote it as written; watch for an errata or FAQ | When seen |

## Engineering questions a lab can answer

| # | Question | What settles it |
|:---|:---|:---|
| E1 | How much do larger handshakes raise latency and failure rates on real networks, mobile and middleboxes included? | A test plan run against isolated endpoints, with p50, p95 and p99 |
| E2 | Does a central mesh change cover service-to-service traffic for most workloads, and what does it miss (non-mesh, custom TLS, external calls)? | A three-hop lab path with negotiated-group logging on each hop |
| E3 | What breaks when a private CA issues ML-DSA certificates to internal relying parties? | A sandbox CA and a compatibility matrix by client library |
| E4 | How does a key ceremony change when the root is ML-DSA, including backup and recovery? | A rehearsal plan with synthetic keys and dual control |
| E5 | Can classical-only fallback be detected and reported without new tooling? | Telemetry design using the platforms' existing negotiated-group fields |

## Questions the company has to answer for itself

These cannot be researched. In this lab they get synthetic answers, clearly labelled.

| # | Question |
|:---|:---|
| C1 | Which data classes must stay confidential for 10 years or more? |
| C2 | How much of the estate is unassessed, and how many services have no owner? |
| C3 | Which HSMs, CAs, appliances and acquired products are in the fleet, at what versions? |
| C4 | Which customers pin certificates, run old clients, or bring their own keys? |
| C5 | Is the company a federal contractor, a FedRAMP provider, or a supplier to national security systems? Each changes the deadlines. |
| C6 | Which shared teams (PKI, HSM, mesh, SRE) are already at capacity? |
