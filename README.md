# Enterprise Post-Quantum Cryptography (PQC) Migration Runbook

This repository provides actionable frameworks, agile sprint models, and compliance checklists for migrating enterprise cryptographic infrastructure to NIST's post-quantum standards (FIPS 203, 204, and 205)[cite: 1, 5]. It is designed for CISOs, security architects, and DevSecOps leads managing the deprecation of RSA and ECC algorithms across legacy systems, third-party supply chains, and zero-trust meshes[cite: 1, 6, 11]. Last updated: June 2026.

## What's in this repo

*   [The NIST 2030 Deadline & HNDL Risk](#the-nist-2030-deadline--hndl-risk)
*   [Crypto-Agility vs. Quantum-Safe Migration](#crypto-agility-vs-quantum-safe-migration)
*   [Building the Cryptographic Bill of Materials (CBOM)](#building-the-cbom--the-eu-2026-mandate)
*   [Agile Sprint Execution & Quantum-Safe Gates](#agile-sprint-execution--quantum-safe-gates)
*   [Securing Machine Identities (SPIFFE & mTLS)](#securing-machine-identities-spiffe--mtls)
*   [`crypto-agility-checklist.md`](crypto-agility-checklist.md) — Step-by-step CISO compliance controls[cite: 1].
*   [`pqc-sprint-backlog.md`](pqc-sprint-backlog.md) — Epic and User Story templates for engineering teams[cite: 4].
*   [`fips-algorithm-cheatsheet.md`](fips-algorithm-cheatsheet.md) — FIPS 203/204/205 mapping and use cases[cite: 5].

---

## The NIST 2030 Deadline & HNDL Risk

Under NIST IR 8547, classical public-key algorithms at the 112-bit security level (like RSA-2048 and ECC P-256) are officially **deprecated after 2030** and completely **disallowed after 2035**[cite: 5]. However, the actual deadline for your enterprise is dictated by "Harvest Now, Decrypt Later" (HNDL) attacks[cite: 5]. Adversaries are currently intercepting and storing encrypted traffic; once cryptographically relevant quantum computers arrive, they will retroactively decrypt these archives[cite: 9, 10]. 

To calculate your actual risk exposure, apply **Mosca's Inequality**:

> If **X** (years your data must remain secret) + **Y** (years it takes to migrate your systems) > **Z** (years until a quantum computer arrives), your data is already exposed[cite: 5].

**Full breakdown:** [The Post-Quantum Migration Playbook NIST Won't Hand CISOs](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/post-quantum-cryptography-crypto-agility-ciso.html)

## Crypto-Agility vs. Quantum-Safe Migration

Treating PQC migration as a 1:1 algorithm swap (e.g., hard-coding ML-KEM where RSA used to be) creates massive technical debt[cite: 2]. If a new NIST standard is later weakened, you will have to repeat the entire multi-year discovery process[cite: 2]. 

*   **Quantum-Safe:** A specific security state achieved by deploying algorithms like ML-KEM[cite: 2].
*   **Crypto-Agility:** An architectural capability achieved by implementing a centralized cryptographic abstraction layer or service mesh[cite: 1, 2]. Applications make API calls to this broker rather than importing standalone crypto libraries, turning future algorithm swaps into simple configuration changes[cite: 1, 2].

**Full breakdown:** [Crypto-Agility vs Quantum-Safe: The Costly Confusion](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/crypto-agility-vs-quantum-safe-migration.html)

## Building the CBOM & The EU 2026 Mandate

You cannot migrate what you cannot see[cite: 5]. The EU Coordinated PQC Roadmap mandates that member states and critical entities complete a comprehensive national cryptographic inventory by **December 2026**, with high-risk use cases fully migrated by 2030[cite: 3]. 

Your first operational move is deploying automated discovery tools across code repositories, compiled binaries, and network traffic to generate a machine-readable Cryptographic Bill of Materials (CBOM)[cite: 1, 3]. Relying on manual audits ensures you will miss cryptography embedded in third-party firmware and internal certificate authorities[cite: 5, 6].

**Full breakdown:** [The EU PQC Roadmap Deadline Most CISOs Will Miss](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/eu-pqc-roadmap-compliance.html)

## Agile Sprint Execution & Quantum-Safe Gates

A multi-year PQC transition executed as a waterfall program will collapse under tangled legacy dependencies[cite: 4, 8]. Treat the migration as a product backlog, prioritizing high-risk/long-lifespan data (like state secrets or patient records) over short-lived session data[cite: 4, 6].

Update your Definition of Done (DoD) immediately to include a **quantum-safe gate**: no new microservice or platform component can ship if it utilizes stand-alone quantum-vulnerable cryptography[cite: 4, 8]. This stops the accumulation of new cryptographic debt while you migrate the legacy estate[cite: 4].

**Full breakdown:** [PQC Migration in Sprints: The Roadmap Auditors Trust](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/pqc-migration-agile-sprint-planning.html)

## Securing Machine Identities (SPIFFE & mTLS)

Zero-trust architectures assume continuous cryptographic verification, but standard SPIFFE Verifiable Identity Documents (SVIDs) currently rely on vulnerable RSA and ECC signatures[cite: 11]. Even though SVID tokens are short-lived, the payloads transferred during mTLS sessions remain permanently vulnerable to HNDL attacks if intercepted today[cite: 11].

Your SPIRE servers must be upgraded to support hybrid cryptographic libraries, issuing SVIDs that contain both classical and post-quantum keys (e.g., ML-DSA) to maintain interoperability during the transition[cite: 11]. 

**Full breakdown:** [SPIFFE + Post-Quantum: The Zero-Trust Gap No One Patches](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/spiffe-post-quantum-zero-trust-integration.html)

---

## Quick Reference Assets

*   [**`crypto-agility-checklist.md`**](crypto-agility-checklist.md) — 10-point implementation and audit checklist for CISO governance[cite: 1].
*   [**`pqc-sprint-backlog.md`**](pqc-sprint-backlog.md) — Ready-to-use Epics and User Stories for engineering teams executing the migration[cite: 4].
*   [**`fips-algorithm-cheatsheet.md`**](fips-algorithm-cheatsheet.md) — Dense mapping of legacy algorithms to their NIST FIPS 203/204/205 replacements[cite: 5].

---

## Sources & Deeper Reading

*   [The Post-Quantum Migration Playbook NIST Won't Hand CISOs](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/post-quantum-cryptography-crypto-agility-ciso.html)
*   [The Crypto-Agility Checklist Before You Touch FIPS 203](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/crypto-agility-ciso-checklist-nist-fips-203-204-205.html)
*   [Crypto-Agility vs Quantum-Safe: The Costly Confusion](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/crypto-agility-vs-quantum-safe-migration.html)
*   [The EU PQC Roadmap Deadline Most CISOs Will Miss](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/eu-pqc-roadmap-compliance.html)
*   [PQC Migration in Sprints: The Roadmap Auditors Trust](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/pqc-migration-agile-sprint-planning.html)
*   [Why Your Post-Quantum Migration Will Miss the 2030 Deadline](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/post-quantum-cryptography-enterprise-migration.html)
*   [Post-Quantum Edge: India’s GCC Strategy](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/post-quantum-cryptography-india-gcc-strategy.html)
*   [Q-Day Prep: The 6 Moves Enterprise Leaders Make First](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/q-day-preparation-enterprise-it-leaders.html)
*   [SPIFFE + Post-Quantum: The Zero-Trust Gap No One Patches](https://agileleadershipdayindia.org/blogs/post-quantum-cryptography-crypto-agility-ciso/spiffe-post-quantum-zero-trust-integration.html)

---

## Contributing / Corrections

If you identify updated NIST parameter recommendations, newly discovered weaknesses in backup algorithms (e.g., HQC), or updates to DORA/NIS2 compliance mappings, please open an issue or submit a PR. This repository is maintained quarterly to align with evolving cryptography standards.

---

**About the Author**

I’m Ayush Bisht, a Content Engineer and AI tools specialist passionate about building smart, scalable, and engaging digital experiences. Currently working with AgileWow, I blend content strategy with AI-driven workflows to create efficient, impactful solutions.

[LinkedIn](https://www.linkedin.com/in/ayush-bisht-92abb1315/).
