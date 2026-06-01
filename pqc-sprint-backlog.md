# Agile Sprint Planning: Post-Quantum Product Backlog

A multi-year cryptographic transition fails as a waterfall project[cite: 4]. Use this backlog structure to segment the migration into auditable, 2-week execution sprints[cite: 4].

## Quantum-Safe Definition of Done (DoD) Gate
*Add this to your team's global DoD:*
> **"No new microservice, application, or platform component may be marked 'Done' if it ships with stand-alone quantum-vulnerable cryptography (RSA/ECC)."**[cite: 4]

---

## Epic 1: Cryptographic Discovery & CBOM Generation
**Description:** Automate the detection of all active cryptographic algorithms across the enterprise to meet EU 2026 mandates[cite: 3, 5].
*   **Story 1.1:** Deploy SAST scanners across Tier 1 (High Secrecy) repositories to detect hardcoded RSA/ECC instances[cite: 1, 6].
*   **Story 1.2:** Implement network traffic analysis tools to map active mTLS cipher suites between internal workloads[cite: 11].
*   **Story 1.3:** Aggregate discovery data into a centralized, machine-readable CBOM database[cite: 3, 5].

## Epic 2: Centralized Cryptographic Abstraction
**Description:** Build the abstraction layer API to decouple application logic from underlying algorithm execution[cite: 1, 2].
*   **Story 2.1:** Develop a centralized signing service to handle all internal JSON Web Token (JWT) generation[cite: 1, 11].
*   **Story 2.2:** Refactor Application A to remove direct imports of `OpenSSL/RSA` and route traffic through the new signing API[cite: 1, 2].
*   **Story 2.3:** Execute DAST scans to ensure Application A successfully processes payloads without falling back to local hardcoded libraries[cite: 1].

## Epic 3: Hybrid Certificate Piloting (SPIRE/mTLS)
**Description:** De-risk the cutover by deploying hybrid certificates in a contained, non-production environment[cite: 4, 11].
*   **Story 3.1:** Upgrade staging SPIRE server to support issuance of hybrid X.509 SVIDs[cite: 11].
*   **Story 3.2:** Deploy hybrid certificates (Classical ECC + ML-DSA) to non-production Workload A and Workload B[cite: 1, 11].
*   **Story 3.3:** Run load testing on Workload A/B mTLS handshakes to measure ML-KEM payload size impact on network latency[cite: 1, 4].

## Recommended Sprint Migration KPIs (For Auditor Reporting)
Avoid static "percentage complete" slides[cite: 4]. Track these per sprint:
1.  Number of legacy libraries replaced by centralized abstraction API calls[cite: 4].
2.  Percentage of CBOM coverage completed[cite: 4].
3.  Number of machine identities (SVIDs) upgraded to hybrid status[cite: 4, 11].
