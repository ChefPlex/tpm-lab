# Sources and Standards Status

**Status:** 🚧 Research, checked **12 October 2026**. Every row was read in the issuing body's own page or document on that date. Standards and products in this area change monthly; recheck any row older than a quarter before relying on it.

**Labels.** **Final** = a published standard or RFC. **Draft** = published for comment or approved and waiting, not yet final. **Vendor-documented** = the supplier's own docs say so; not tested here. **Unverified** = a source exists but the exact wording was not confirmed. **Guidance** = not binding on anyone.

## What a program can plan against today

| Question | Short answer, as of 12 Oct 2026 |
|:---|:---|
| Are the replacement algorithms final? | **Yes.** ML-KEM, ML-DSA and SLH-DSA, all August 2024. |
| Can TLS use them for key exchange? | **Yes.** Hybrid groups are a Proposed Standard RFC (August 2026), and Chrome, Firefox, Apple's OS 26 family, OpenSSL 3.5 and Go already offer them by default. |
| Can TLS use them for certificates and server authentication? | **Not yet.** The ML-DSA-in-TLS document is approved but not published; Merkle Tree Certificates are a working-group draft. Browsers have a roadmap with no dates. |
| Can a private CA issue post-quantum certificates? | **Standards yes** (ML-DSA, SLH-DSA and ML-KEM in X.509 are RFCs). Relying-party support is the open question. |
| Is there a FIPS 140-3 validated module with ML-KEM and ML-DSA? | **Yes, at least one HSM.** Most libraries and HSM lines are still in validation. |
| When do the old algorithms go away? | **No final NIST date.** NIST's transition plan is still a 2024 draft proposing "deprecated after 2030" (112-bit strength only) and "disallowed after 2035". |
| Who is legally required to migrate? | **US federal agencies and national security systems.** Contractors are next, through a planned acquisition rule. Everyone else is guidance or contract. |

## 1. Algorithms (NIST)

| Item | Document | Date | Status | Function | Source |
|:---|:---|:---|:---|:---|:---|
| ML-KEM | FIPS 203 | 2024-08-13 | Final; errata pending (note of 2025-11-17) | Key establishment | [csrc.nist.gov](https://csrc.nist.gov/pubs/fips/203/final) |
| ML-DSA | FIPS 204 | 2024-08-13 | Final; errata pending (note of 2026-07-31) | Signatures | [csrc.nist.gov](https://csrc.nist.gov/pubs/fips/204/final) |
| SLH-DSA | FIPS 205 | 2024-08-13 | Final | Signatures (hash-based) | [csrc.nist.gov](https://csrc.nist.gov/pubs/fips/205/final) |
| Extra SLH-DSA parameter sets | SP 800-230 | 2026-04-13 | Draft, comments closed | Signatures | [csrc.nist.gov](https://csrc.nist.gov/pubs/sp/800/230/ipd) |
| FN-DSA (Falcon) | FIPS 206 | none | **No public draft found** | Signatures | [CSRC FIPS list](https://csrc.nist.gov/publications/fips) |
| HQC (backup KEM) | none yet | selected 2025-03-11 | Selected; NIST planned a draft "in about a year" and a final in 2027. No draft found. | Key establishment | [nist.gov](https://www.nist.gov/news-events/news/2025/03/nist-selects-hqc-fifth-algorithm-post-quantum-encryption) |
| KEM guidance, including hybrids | SP 800-227 | 2025-09-18 | Final. Section 4.6 covers hybrid "PQ/T" key establishment and the approved ways to combine keys | Key establishment | [csrc.nist.gov](https://csrc.nist.gov/pubs/sp/800/227/final) |
| Crypto agility | CSWP 39 upd1 | 2025-12-19, updated 2026-06-29 | Final | All | [csrc.nist.gov](https://csrc.nist.gov/pubs/cswp/39/upd1/considerations-for-achieving-crypto-agility/final) |
| Transition timeline | IR 8547 ipd | 2024-11-12 | **Still the initial public draft.** Proposes 112-bit RSA, ECDSA, DH and ECDH "deprecated after 2030" and all quantum-vulnerable public-key algorithms "disallowed after 2035" | All public-key | [csrc.nist.gov](https://csrc.nist.gov/pubs/ir/8547/ipd) |
| Additional signatures | On-ramp Round 3 | 2026-05-14 | Nine advanced; HAWK withdrawn by its team on 2026-07-29 after a reported vulnerability; about two years remaining | Signatures | [nist.gov](https://www.nist.gov/news-events/news/2026/05/nine-candidates-advance-third-round-additional-digital-signatures-pqc) |
| Stateful hash-based signatures (LMS, XMSS) | SP 800-208 | 2020-10-29 | Final; "not suitable for general use", fit for firmware signing | Signatures | [csrc.nist.gov](https://csrc.nist.gov/pubs/sp/800/208/final) |
| Cryptographic discovery | SP 1800-38 (NCCoE) | 2023-12-19 | Preliminary draft (Volumes B and C); project page not reachable on the check date | Inventory | [csrc.nist.gov](https://csrc.nist.gov/pubs/sp/1800/38/iprd-(1)) |

**Sizes a planner needs** (bytes, from FIPS 203 and 204): ML-KEM-768 public key 1,184 and ciphertext 1,088. ML-DSA-65 public key 1,952 and signature 3,309. For comparison, an X25519 key share is 32 bytes. Larger handshakes and certificates are the source of most compatibility work.

## 2. Protocols (IETF and implementations)

| Item | Document | Date | Status | Source |
|:---|:---|:---|:---|:---|
| Hybrid key exchange for TLS 1.3: X25519MLKEM768 (0x11EC, recommended), SecP256r1MLKEM768, SecP384r1MLKEM1024 | RFC 10024 | Aug 2026 | Final (Proposed Standard) | [rfc-editor.org](https://www.rfc-editor.org/info/rfc10024) |
| Hybrid key exchange design for TLS 1.3 | RFC 9954 | Jul 2026 | Final (Informational). TLS only, not a general KEM framework | [rfc-editor.org](https://www.rfc-editor.org/info/rfc9954) |
| Pure ML-KEM groups for TLS | draft-ietf-tls-mlkem | 2026 | Draft, approved, in the RFC Editor queue | [datatracker](https://datatracker.ietf.org/doc/draft-ietf-tls-mlkem/) |
| ML-DSA for TLS authentication | draft-ietf-tls-mldsa | 2026 | Draft, approved, in the RFC Editor queue | [datatracker](https://datatracker.ietf.org/doc/draft-ietf-tls-mldsa/) |
| Merkle Tree Certificates | draft-ietf-plants-merkle-tree-certs | 2026-10-07 | Working-group draft | [datatracker](https://datatracker.ietf.org/doc/draft-ietf-plants-merkle-tree-certs/) |
| ML-DSA in X.509 | RFC 9881 | Oct 2025 | Final | [rfc-editor.org](https://www.rfc-editor.org/info/rfc9881) |
| SLH-DSA in X.509 | RFC 9909 | Dec 2025 | Final | [rfc-editor.org](https://www.rfc-editor.org/info/rfc9909) |
| ML-KEM in X.509 | RFC 9935 | Mar 2026 | Final | [rfc-editor.org](https://www.rfc-editor.org/info/rfc9935) |
| KEMs in CMS; ML-KEM in CMS | RFC 9629; RFC 9936 | Aug 2024; Mar 2026 | Final | [rfc-editor.org](https://www.rfc-editor.org/info/rfc9936) |
| Composite (hybrid) signatures for X.509 | draft-ietf-lamps-pq-composite-sigs | 2026 | Draft, approved, being edited | [datatracker](https://datatracker.ietf.org/doc/draft-ietf-lamps-pq-composite-sigs/) |
| ML-DSA for JOSE and COSE (signed tokens) | RFC 9964 | May 2026 | Final | [rfc-editor.org](https://www.rfc-editor.org/info/rfc9964) |
| PQ KEMs and SLH-DSA for JOSE/COSE | two drafts | 2026 | Drafts | [datatracker](https://datatracker.ietf.org/doc/draft-ietf-jose-pqc-kem/) |
| SSH hybrid ML-KEM key exchange | RFC 10042 | Aug 2026 | Final (Informational). OpenSSH default since 10.0 (April 2025); 10.1 warns on non-PQ key exchange | [rfc-editor.org](https://www.rfc-editor.org/info/rfc10042) · [openssh.com](https://www.openssh.com/pq.html) |
| IKEv2 multiple key exchanges; ML-KEM in IKEv2 | RFC 9370; draft-ietf-ipsecme-ikev2-mlkem | May 2023; 2026 | Final; draft in the RFC Editor queue | [rfc-editor.org](https://www.rfc-editor.org/info/rfc9370) |
| Browser authentication roadmap | Chromium | 2026-02-27 | Four stages, **no dates** | [chromium.org](https://www.chromium.org/Home/chromium-security/post-quantum-auth-roadmap/) |
| Let's Encrypt Merkle Tree Certificates | blog | 2026-06-03 | Plan: staging late 2026, production 2027 | [letsencrypt.org](https://letsencrypt.org/2026/06/03/pq-certs) |
| Client defaults | Apple OS 26 family; Firefox; Chrome 131 | 2024 to 2026 | Vendor-documented: all offer X25519MLKEM768 | [Apple](https://support.apple.com/en-us/122756) · [Mozilla](https://firefox-admin-docs.mozilla.org/reference/policies/postquantumkeyagreementenabled/) · [Google](https://security.googleblog.com/2024/09/a-new-path-for-kyber-on-web.html) |

**QUIC note.** QUIC carries the same TLS 1.3 groups. The X25519MLKEM768 client share alone is 1,216 bytes, more than QUIC's 1,200-byte minimum first datagram, so the first handshake message spans several packets. That is arithmetic from RFC 10024 and RFC 9000; specific middlebox failures were not checked.

## 3. Government and regulation

| Item | Issuer | Date | Binding? | Who | Key dates | Source |
|:---|:---|:---|:---|:---|:---|:---|
| EO 14412, Securing the Nation Against Advanced Cryptographic Attacks | US President | 2026-06-22 | Yes, on the executive branch | Federal agencies; FAR Council told to propose a rule binding **covered contractors** to PQC-inclusive FIPS by **2030-12-31** | Key establishment 2030-12-31; signatures 2031-12-31; FAR proposed rule due about 2026-12-19 (none published as of 12 Oct) | [whitehouse.gov](https://www.whitehouse.gov/presidential-actions/2026/06/securing-the-nation-against-advanced-cryptographic-attacks/) · [Federal Register](https://www.federalregister.gov/documents/2026/06/25/2026-12909/securing-the-nation-against-advanced-cryptographic-attacks) |
| OMB M-26-15, Execution of the Migration to PQC | OMB | 2026-06-24 | Yes, on agencies | Federal civilian agencies, not national security systems | Plans due about 2026-10-22; phases 2026 to 2035; TLS 1.3 by 2030-01-02; agencies to engage FedRAMP cloud providers | [whitehouse.gov PDF](https://www.whitehouse.gov/wp-content/uploads/2026/06/M-26-15-Execution-of-the-Migration-to-Post-Quantum-Cryptography.pdf) |
| OMB M-23-02 | OMB | 2022-11-18 | Yes, on agencies | Federal agencies | Annual inventory to 2035 | [whitehouse.gov PDF](https://www.whitehouse.gov/wp-content/uploads/2022/11/M-23-02-M-Memo-on-Migrating-to-Post-Quantum-Cryptography.pdf) |
| NSM-10 | US President | 2022-05-04 | Yes, on the executive branch | Agencies and NSS owners | 2035 goal | [archives](https://bidenwhitehouse.archives.gov/briefing-room/statements-releases/2022/05/04/national-security-memorandum-on-promoting-united-states-leadership-in-quantum-computing-while-mitigating-risks-to-vulnerable-cryptographic-systems/) |
| CNSA 2.0 (via CNSSP 15) | NSA / CNSS | FAQ v2.1, Dec 2024 | Yes, for national security systems | NSS owners and their suppliers | New acquisitions 2027-01-01; phase-out 2030-12-31; mandatory 2031-12-31; all NSS by 2035. Uses ML-KEM-1024 and ML-DSA-87 | [NSA FAQ](https://media.defense.gov/2022/Sep/07/2003071836/-1/-1/1/CSI_CNSA_2.0_FAQ_.PDF) · [NSA, 2026-10-01](https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/4615285/nsa-announces-post-quantum-cryptography-measures-to-safeguard-national-security/) |
| PQC product categories | CISA | 2026-01-23 | Procurement guidance to agencies | Federal buyers | PaaS, IaaS, browsers and web servers "widely available"; **SaaS "transitioning"** | [cisa.gov](https://www.cisa.gov/resources-tools/resources/product-categories-technologies-use-post-quantum-cryptography-standards) |
| Preparing for the Post-Quantum Era: A Call to Action | CISA and the G7 Cyber Security Working Group | 2026-09-03 | Guidance | Nobody | Five priorities, no deadlines | [cisa.gov](https://www.cisa.gov/resources-tools/resources/preparing-post-quantum-era-call-action) |
| PQC migration timelines | UK NCSC | 2025-03-20 | Guidance ("indicative") | Nobody directly | 2028 discovery and plan; 2031 priority migration; 2035 complete | [ncsc.gov.uk](https://www.ncsc.gov.uk/guidance/pqc-migration-timelines) |
| Coordinated roadmap | EU NIS Cooperation Group | 2025-06-23 | Recommendation | Member States, for public bodies and critical infrastructure | End-2026 first steps; end-2030 high-risk; end-2035 medium-risk | [digital-strategy.ec.europa.eu](https://digital-strategy.ec.europa.eu/en/library/coordinated-implementation-roadmap-transition-post-quantum-cryptography) |
| Federal roadmap | Canada CCCS | June 2025 | Guidance for departments | Government of Canada, non-classified | High-priority systems end-2031; rest end-2035 | [cyber.gc.ca](https://www.cyber.gc.ca/en/guidance/roadmap-migration-post-quantum-cryptography-government-canada-itsm40001) |
| Planning for PQC | Australia ASD | reviewed 2025-09-22 | ISM guidance | ISM users | **Stop traditional asymmetric cryptography by end-2030**, the earliest date found | [cyber.gov.au](https://www.cyber.gov.au/publication/planning-for-post-quantum-cryptography) |

**How a commercial SaaS company gets pulled in:** federal contracts (the planned FAR rule), FedRAMP (M-26-15 tells agencies to agree PQC responsibilities with their cloud providers), national security customers (CNSA 2.0 levels), and customers in regulated sectors who copy these dates into supplier questionnaires.

## 4. Products and suppliers

**Vendor-documented** unless a certificate number is given. "Supports the algorithm" and "FIPS 140-3 validated module" are different claims.

| Supplier and product | Version | What it does | Function | Status | FIPS context | Source |
|:---|:---|:---|:---|:---|:---|:---|
| OpenSSL | 3.5 (Apr 2025), LTS to 2030 | ML-KEM, ML-DSA, SLH-DSA; X25519MLKEM768 in the default key share | Both | Released | The project's validated provider is 3.1.2; the 3.5 provider is in CMVP review | [openssl-library.org](https://openssl-library.org/news/openssl-3.5-notes/) |
| Go | 1.24 | X25519MLKEM768 on by default | Key establishment | Released | Not checked | [go.dev](https://go.dev/doc/go1.24) |
| Kubernetes | 1.33 | Hybrid TLS by default, inherited from Go 1.24 | Key establishment | Released | n/a | [kubernetes.dev](https://kubernetes.dev/blog/2025/07/18/pqc-in-k8s/) |
| Java; .NET | JDK 24; .NET 10 | ML-KEM and ML-DSA APIs (.NET marks SLH-DSA and composite as experimental) | Both | Released | Not checked | [openjdk.org](https://openjdk.org/jeps/496) · [Microsoft](https://devblogs.microsoft.com/dotnet/post-quantum-cryptography-in-dotnet/) |
| Envoy | 1.40 (unreleased) | X25519MLKEM768 in default curves on `main`; 1.39 can log the negotiated group | Key establishment | **Default not yet in a release** | "FIPS builds" is a build flavour, not validation | [github.com/envoyproxy](https://github.com/envoyproxy/envoy/blob/main/docs/root/intro/arch_overview/security/ssl.rst) |
| Istio | 1.27+ | `COMPLIANCE_POLICY=pqc` forces TLS 1.3 and X25519MLKEM768 | Key establishment | **Experimental** | Separate from the FIPS policies | [github.com/istio](https://github.com/istio/istio/blob/master/pkg/features/security.go) |
| AWS KMS | all Regions | Hybrid PQ TLS on all endpoints; CloudTrail shows the negotiated group | Key establishment | Generally available | Available on FIPS endpoints | [docs.aws.amazon.com](https://docs.aws.amazon.com/kms/latest/developerguide/pqtls.html) |
| AWS KMS | ML-DSA-44/65/87 | Signing keys | Signatures | Generally available (Jun 2025) | Keys held in validated HSMs; certificate boundary not checked | [docs.aws.amazon.com](https://docs.aws.amazon.com/kms/latest/developerguide/mldsa.html) |
| AWS Secrets Manager clients | Agent 2.0.0+ and others | Hybrid PQ TLS by default | Key establishment | Generally available (Apr 2026) | Not stated | [aws.amazon.com](https://aws.amazon.com/about-aws/whats-new/2026/04/aws-secrets-manager-post-quantum-tls/) |
| AWS CloudHSM | SDK 5.18.0, hsm2m.medium | ML-DSA keys, sign, verify | Signatures | FIPS mode from 2026-09-01 | No certificate checked | [docs.aws.amazon.com](https://docs.aws.amazon.com/cloudhsm/latest/userguide/cloudhsm_cli-key-generate-asymmetric-pair-mldsa.html) |
| Google Cloud KMS | software keys only | ML-DSA, SLH-DSA | Signatures | Generally available (release notes 2026-07-16) | No HSM protection level | [cloud.google.com](https://docs.cloud.google.com/kms/docs/release-notes) |
| Google Cloud KMS | software keys only | ML-KEM-768, ML-KEM-1024, X-Wing | Key establishment | **Preview** in the release notes; a July 2026 blog says GA. The sources conflict. | None stated | [cloud.google.com](https://docs.cloud.google.com/kms/docs/algorithms) |
| Google Cloud Load Balancing | 7 load balancer types | X25519MLKEM768 | Key establishment | Opt-in; default from October 2026; always on after October 2027 | Not stated | [cloud.google.com](https://docs.cloud.google.com/load-balancing/docs/post-quantum-tls) |
| Thales Luna T7 | CMVP **#5450** | ML-KEM and ML-DSA as approved algorithms | Both | Validated 2026-07-29, FIPS 140-3 Level 3 | **Validated** | [csrc.nist.gov](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5450) |
| Entrust nShield 5s | CMVP #5329 | Current certificate lists **no** PQC algorithms; PQC firmware in CMVP review | Both (vendor claim) | Not validated for PQC | In review | [csrc.nist.gov](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/5329) |
| Utimaco u.trust | Quantum Protect | ML-KEM, ML-DSA, LMS | Both (vendor claim) | Algorithm tests passed (CAVP); module in validation | Not validated | [utimaco.com](https://utimaco.com/news/blog-posts/utimacos-nist-validated-pqc-algorithms-setting-standard-future-data-security) |
| Cloudflare | edge | Over half of human traffic PQ-protected (Oct 2025); PQ to origins opt-in | Key establishment | Generally available | n/a | [blog.cloudflare.com](https://blog.cloudflare.com/pq-2025/) |
| CycloneDX | 1.6 (Apr 2024) | Cryptographic bill of materials (CBOM): algorithms, keys, certificates | Inventory | Released | n/a | [cyclonedx.org](https://cyclonedx.org/capabilities/cbom/) |
| IBM sonar-cryptography | current | Scans Java, Python and Go source, emits a CycloneDX CBOM | Inventory | Released | n/a | [github.com/IBM](https://github.com/IBM/sonar-cryptography) |
| Sigstore | spec | ML-DSA in the spec; public instance not PQ yet | Signatures | Experimental | n/a | [blog.sigstore.dev](https://blog.sigstore.dev/post-quantum-2025/) |

## Not checked

Recorded so a gap reads as a gap: the contents of the FIPS 203 and 204 errata; the NCCoE project page (blocked); the original 2022 CNSA 2.0 per-category timeline (the PDF has moved, and NSA's current FAQ gives the CNSSP 15 dates instead); Germany's BSI and the Netherlands; Chrome and Firefox version histories; the live Cloudflare Radar figure for 2026; whether the AWS or Google ML-DSA keys sit inside a validation certificate; Azure. Some cloud release-note quotes came through a page extractor and should be reread before being quoted elsewhere.
