# Post-Quantum Cryptography

**Status:** 🚧 In progress: research

How you would upgrade cryptography across a very large enterprise, many clouds, many engineering teams and hundreds of services, for the move to post-quantum algorithms. The enterprise is generic: no specific company's systems or figures appear here.

This is a migration program, not quantum key distribution. The work is finding everywhere the current public-key algorithms are used and moving it to the newer standardized ones, without breaking the services that depend on it.

## What Will Be Here

- **Research notes**: the standards, the official migration guidance and timelines, each linked and dated.
- **Program charter**: problem, outcomes, owners, scope.
- **Phased plan**: from finding where cryptography is used, through the migration, to proving it is done.
- **Cryptographic inventory template**: the record of what uses which algorithm, where, and who owns it.

## Related

- [Encryption Program Playbook](https://github.com/ChefPlex/security-program-playbooks/blob/main/encryption-program-playbook.md)
- [Lessons from Leading Large-Scale Encryption Programs](https://github.com/ChefPlex/learning-notes/blob/main/lessons-from-large-scale-encryption-programs.md)
- [Cryptography Fundamentals for TPMs](https://github.com/ChefPlex/learning-notes/blob/main/cryptography-fundamentals-for-tpms.md)
