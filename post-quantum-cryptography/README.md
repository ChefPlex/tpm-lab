# Post-Quantum Cryptography

**Status:** 🚧 In progress: research checked October 2026; charter and first-90-days plan in first draft

How you would upgrade cryptography across a very large enterprise, many clouds, many engineering teams and hundreds of services, for the move to post-quantum algorithms. The enterprise is fictional, **Meridian Cloud Systems**: no specific company's systems or figures appear here.

This is a migration program, not quantum key distribution. The work is finding everywhere the current public-key algorithms are used and moving it to the newer standardized ones, without breaking the services that depend on it.

## The model in one paragraph

Confidentiality can move now; authentication cannot, yet. Hybrid post-quantum key exchange for TLS is a published standard that browsers, OpenSSL, Go and the major clouds already use, while post-quantum certificates for servers are still drafts. So the program runs two tracks with separate definitions of done. Before either, it finds what cryptography is in use, on which hop, owned by whom, because one upgraded hop does not protect a data path and a capable server protects nothing until clients negotiate with it. Central platforms carry most of the change, teams adopt them, and the lasting result is the ability to change algorithms again without another multiyear program.

## What Is Here

| File | What it is |
|:---|:---|
| [What the Research Says](research-findings.md) | What is ready now and what is not, the threat model, and where lessons from earlier encryption programs land |
| [Sources and Standards Status](sources.md) | Every standard, RFC, government rule and supplier capability, with status and date |
| [Program Charter](charter.md) | First draft: problem, outcomes by cryptographic function, scope, guardrails, decision rights |
| [The First 90 Days](first-90-days.md) | Weeks 1 to 4 in full, weeks 5 to 13 in outline, and the three gates |
| [Open Questions](open-questions.md) | What the research could not settle, and what would settle it |
| [Backlog and Work Log](backlog.md) | The next ten pieces of work, with what "done" means |

Still to come: the inventory model and a synthetic inventory, architecture decision records, the capacity model, test plans, metrics, and the multiyear roadmap.

## Related

- [Encryption Program Playbook](https://github.com/ChefPlex/security-program-playbooks/blob/main/encryption-program-playbook.md)
- [Lessons from Leading Large-Scale Encryption Programs](https://github.com/ChefPlex/learning-notes/blob/main/lessons-from-large-scale-encryption-programs.md)
- [Cryptography Fundamentals for TPMs](https://github.com/ChefPlex/learning-notes/blob/main/cryptography-fundamentals-for-tpms.md)
