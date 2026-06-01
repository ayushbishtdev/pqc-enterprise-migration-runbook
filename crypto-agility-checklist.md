# CISO Crypto-Agility & PQC Implementation Checklist

This checklist maps directly to the operationalization of NIST FIPS 203, 204, and 205[cite: 1]. Use this to ensure your architecture is abstracted *before* deploying new algorithms[cite: 1].

### 1. Discovery & Inventory (CBOM)
- [ ] **Deploy Automated Discovery:** Implement tools to scan code repos, network traffic, and binaries for algorithm types and key lengths[cite: 1].
- [ ] **Generate CBOM:** Compile a machine-readable Cryptographic Bill of Materials mapping every cryptographic dependency[cite: 1, 5].
- [ ] **Rank by Mosca's Inequality:** Prioritize systems based on data-secrecy lifespan (X) against migration time (Y)[cite: 5, 6].

### 2. Cryptographic Abstraction Layer
- [ ] **Ban Hardcoding:** Enforce strict governance forbidding developers from directly importing standalone cryptographic libraries[cite: 1].
- [ ] **Deploy API Brokers:** Route all encryption/signing requests through a centralized service broker to decouple business logic from crypto execution[cite: 1, 2].
- [ ] **SAST/DAST Verification:** Configure security testing tools to flag explicitly declared legacy algorithms (RSA, ECC) in source code[cite: 1].

### 3. Key Lifecycle Automation
- [ ] **Upgrade CA/HSMs:** Ensure your Certificate Authorities and Hardware Security Modules support hybrid certificate issuance[cite: 1].
- [ ] **Automate Rotation:** Implement tooling for rapid, automated cycling of both short-lived machine identities (SVIDs) and long-term storage keys[cite: 1, 11].

### 4. Pilot & Hybrid Deployment
- [ ] **Deploy Hybrid Key Exchange:** Combine FIPS 203 (ML-KEM) alongside a classical algorithm (like ECC) in a strictly contained environment[cite: 1].
- [ ] **Monitor Latency:** Benchmark hybrid deployments for performance latency and payload size issues without risking operational downtime[cite: 1, 4].

### 5. Audit & Compliance 
- [ ] **Centralize Logs:** Route all abstraction layer API calls to a centralized logging system to create immutable proof of algorithm usage[cite: 1].
- [ ] **Map to Frameworks:** Align automated key rotation logs directly with ISO 27001, NIS2, and DORA control requirements for external auditors[cite: 1, 3].
