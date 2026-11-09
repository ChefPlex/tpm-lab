# Backlog and Work Log

**Status:** 🚧 Live, October 2026. What comes next in this lab, in order, with what "done" means for each.

## Next ten

| # | Priority | Item | Done when | Depends on |
|:---|:---|:---|:---|:---|
| 0 | P0, first | **Scope by network zone** | Every data path in scope is classed by the networks it crosses: (a) **internal**, where we control both ends, so the easiest to move; (b) **the internet**, where we control one end and must stay backward compatible with weaker cryptography, so a fallback and exception policy is needed; (c) **the customer's own network**, which we do not control at all. Other zones are listed too (partners and suppliers, cloud provider backbones, third-party services). The charter states which zones are in scope, and the exposure where one leg of a path moves to post-quantum and another does not is written down per path | Charter draft |
| 1 | P0 | **Inventory data model and denominator policy** | Schema for services, assets, flows, hops, observations, keys and certificates, owners, exceptions and scope changes; evidence states defined; a scope-change log format | [research-findings.md](research-findings.md) |
| 1a | P0 | **Discovery: what cryptography actually exists today** | Every discovery source in [first-90-days.md](first-90-days.md) week 3 has been pulled at least once, and a baseline shows, per network zone, the algorithms, key sizes, protocol versions, certificates and libraries actually in use. Each entry is marked observed or self-reported, unknowns are counted rather than dropped, and the output is a cryptographic bill of materials (CycloneDX CBOM) where a tool can emit one | Items 0 and 1 |
| 1b | P0 | **Risk tiers and risk register** | ✅ First draft: [risk-register.md](risk-register.md). Exposure tiers T1 to T4 by decision table, a delivery register v0 of 11 rows, synthetic exposure examples. Next: reviewed, and wired to the scorecards (item 8) | Items 0 and 1 |
| 2 | P0 | **Weeks 5 to 13 of the 90-day plan in full** | Each week has objective, meetings, tasks, outputs, done-when, decision and blocker trigger, like weeks 1 to 4 | Charter draft |
| 3 | P0 | **Trust-boundary diagram for one data path** | A Mermaid diagram that renders on GitHub, every hop labelled with protocol, function, owner and evidence state | Item 1 |
| 4 | P1 | **Five architecture decision records** | Hybrid TLS profile; central mesh versus app-by-app; separate signature track; HSM upgrade versus replace; fallback and exception sunset. Each with options, evidence, decision owner, revisit trigger | [sources.md](sources.md) |
| 5 | P1 | **Capacity and bottleneck model** | The PKI, HSM and mesh teams named with capacity; one example where adding people does not move the date | Item 1 |
| 6 | P1 | **Hybrid TLS lab test plan** | Advertised versus negotiated group, fallback, middlebox and size cases, success and stop rules. Marked "specification, not run" until it is run | Item 4 |
| 7 | P1 | **Exception and rollback policy** | Exception fields, expiry, approver by risk tier; one denied example; rollback opens an exception automatically | Charter |
| 8 | P1 | **Scorecard definitions** | Each metric with numerator, versioned denominator, source, owner, freshness and known bias; confidentiality and authentication reported separately | Item 1 |
| 9 | P2 | **Synthetic inventory and an offline checker** | 30 to 75 synthetic records carrying the six scenario threads; a small standard-library script that validates them and computes per-hop and per-path coverage, with a test that fails when coverage rises only because the denominator shrank | Items 1 and 8 |
| 10 | P2 | **Supplier and partner questionnaire** | Versioned questions that separate announced, preview and generally available, and algorithm support from module validation. Partners (who run their own end of a path) get the same questions plus a roadmap date, and a missing date is escalated, not waited on | [sources.md](sources.md) §4 |
| 11 | P1 | **Working group charter with named owners** | One page: each engineering domain (edge, mesh, data, identity, PKI and HSM, client SDKs), plus GRC, Legal and procurement, has one named owner and a deputy; what the group decides versus escalates; how a member is replaced | Charter |
| 12 | P1 | **Decision framework for engineering teams** | A one-page guide a team uses without the TPM: is my path covered by a platform default, a library upgrade, or a team change; when do I need an exception; who approves. Tested by walking the four synthetic exposure rows through it | Items 1b and 4 |
| 13 | P1 | **Test and release dependency map** | For each cohort: which platform release a team must wait for, the canary order across teams, shared test environments, and the rollback path. Shows where two teams' releases must land together | Items 5 and 6 |
| 14 | P2 | **Executive dashboard mock** | The monthly view in [risk-register.md](risk-register.md), drawn with synthetic numbers: T1 paths observed protected on every hop, exceptions expiring, delivery risks needing a decision, conditionals, unknowns | Items 1b and 8 |

Later: multiyear roadmap with the two tracks drawn separately, business case with base, accelerated and constrained scenarios, tabletop exercises, steering pack, handoff to permanent operations.

## Work log

| Date | What changed |
|:---|:---|
| 2026-11-09 | Added item 1b, risk tiers and the risk register (first draft), and items 11 to 14: working group charter, decision framework for teams, test and release dependency map, executive dashboard mock. Item 10 now covers partners as well as suppliers. Symmetric ciphers and hashing are now named in scope for the inventory. |
| 2026-10-16 | Added item 1a, discovery of what cryptography exists today. Week 3 already plans the sources; nothing in the backlog ran them or produced the baseline. |
| 2026-10-16 | Added item 0, scope by network zone: a path is only as protected as its weakest network, and internal, internet and customer networks move at different speeds with different levels of control. |
| 2026-10-12 | Research pass against primary sources (NIST, IETF, US and international government, suppliers). Added sources, research findings, open questions, charter draft, first-90-days draft and this backlog. |

## Review checklist

- [ ] No real company named as the subject; Meridian Cloud Systems only, labelled fictional
- [ ] Every number in an example labelled synthetic
- [ ] No claim about any real company's internal systems or readiness
- [ ] Every source link opens, and its date is in [sources.md](sources.md)
- [ ] Draft versus final status rechecked for anything older than a quarter
- [ ] No long verbatim copying from sources; quotes are short and attributed
- [ ] Status lines say "in progress" until the charter and plan are reviewed
