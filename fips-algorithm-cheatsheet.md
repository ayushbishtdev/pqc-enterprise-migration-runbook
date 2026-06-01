# NIST Post-Quantum Cryptography Cheatsheet

Reference guide for mapping deprecated classical cryptography to NIST's finalized post-quantum standards[cite: 5]. 

| Legacy Algorithm (Deprecated >2030) | Purpose | NIST PQC Standard | Underlying Math | Enterprise Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **RSA / ECDH** | Key Exchange & Encapsulation | **ML-KEM (FIPS 203)** | Module-Lattice | Establishing shared secrets for TLS, VPNs, and mTLS mesh networks. Migrate this first[cite: 5, 11]. |
| **RSA / ECDSA** | Digital Signatures | **ML-DSA (FIPS 204)** | Module-Lattice | General authentication, JSON Web Tokens (JWTs), standard X.509 certificates, SVIDs[cite: 5, 11]. |
| **RSA (Large Key)** | High-Longevity Signatures | **SLH-DSA (FIPS 205)** | Stateless Hash-Based | Code signing, firmware signing, root CAs. Slower/larger signatures, but highly conservative security[cite: 1, 5]. |
| **(None)** | Backup Key Encapsulation | **HQC** | Code-Based | Secondary KEM selected by NIST to provide architectural diversity if lattice math is compromised[cite: 5]. |

## Key Timelines (NIST IR 8547 & EU Roadmap)
*   **2026 (December):** EU mandate for completed national cryptographic inventories and transition plans[cite: 3].
*   **2030:** RSA and ECC (112-bit) are officially **deprecated** by NIST. Unsafe for new deployments[cite: 5, 10]. High-risk EU systems must be fully migrated[cite: 3].
*   **2035:** RSA and ECC are **disallowed** by NIST. Certificates relying on them lose trust[cite: 5, 10].
