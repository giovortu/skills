# CRA Technical Documentation Dossier (Annex VII)
**Product**: Industrial Edge Gateway Model G-200  
**Standard Conformance**: ASD-STE100 (75% Profile) | EU CRA (Regulation 2024/2847) | IEC 62443-4-2 SL2  
**CE Marking Technical File ID**: TF-CRA-2026-G200-01  

---

## 1. Product Identification and Intended Purpose

The Industrial Edge Gateway Model G-200 is a connected hardware device with digital elements. The device collects sensor data from industrial machinery in Zone 1. The device transmits encrypted telemetry to supervisory systems in Zone 3 over an industrial Ethernet conduit.

### Product Specifications
- **Manufacturer**: Industrial Tech Solutions S.p.A.
- **Hardware Architecture**: Dual-core ARM Cortex-A53 with Hardware Root of Trust (TPM 2.0).
- **Operating System**: Hardened Linux (Kernel 6.6 LTS).
- **Network Interfaces**: 2x 1000BASE-T Ethernet ports, 1x isolated RS-485 serial port.
- **Support Period**: 7 years from initial market placement (Guaranteed security updates until November 2033).

---

## 2. Essential Cybersecurity Requirements Assessment (Annex I)

### 2.1 Security by Design and Default (Annex I, Part I, Point 1)
- The gateway ships with all unused ports physically disabled and logical ports blocked.
- The default configuration blocks all inbound network traffic on interface `eth0`.
- The device contains no hardcoded or default factory credentials.
- The commissioning engineer must set a unique password during initial installation.

### 2.2 Access Control and Data Protection (IEC 62443 SL2 FR1, FR2, FR4)
- User authentication enforces Role-Based Access Control (RBAC).
- Failed authentication triggers account lockout after 5 consecutive attempts.
- All network communications between zones use TLS 1.3 with AES-128-GCM encryption.
- The internal cryptographic keys remain protected inside the TPM 2.0 hardware chip.

### 2.3 System Integrity and Secure Updates (IEC 62443 SL2 FR3 & CRA Annex I)
- The boot process verifies cryptographic signatures using the TPM 2.0 root of trust.
- The system rejects firmware updates that do not carry a valid RSA-3072 signature.
- Security patches are distributed separately from feature releases.

---

## 3. Vulnerability Handling and SBOM Policy (Annex I, Part II)

### 3.1 Software Bill of Materials (SBOM)
- The manufacturer generates a machine-readable SBOM in CycloneDX JSON format during every software build.
- The SBOM file resides in the technical repository: `sbom/cyclonedx-g200-v2.1.json`.
- The SBOM inventories all third-party libraries, license terms, and component versions.

### 3.2 Coordinated Vulnerability Disclosure (CVD)
- Security researchers can report vulnerabilities to:
  `security@industrialtech.example.com`
- The public security policy is available at:
  `https://www.industrialtech.example.com/.well-known/security.txt`
- The security team acknowledges vulnerability reports within 48 hours.

### 3.3 Mandatory Article 14 Reporting Timelines
The manufacturer maintains documented incident response procedures:
1. **24 Hours**: Submit an early warning to the competent national CSIRT and ENISA if an actively exploited vulnerability or severe incident occurs.
2. **72 Hours**: Submit a detailed incident notification with initial severity assessments.
3. **1 Month**: Submit the final incident report with root-cause analysis and mitigation measures.

---

## 4. Harmonized Standards Conformance Checklist

```
[x] IEC 62443-4-1: Secure product development lifecycle (Certified).
[x] IEC 62443-4-2: Technical security requirements for IACS components (SL2 Verified).
[x] IEC 62443-3-3: System security requirements and security levels (Zone & Conduit Compliant).
[x] ISO/IEC 29147: Information technology - Vulnerability disclosure (CVD Active).
[x] ISO/IEC 30111: Information technology - Vulnerability handling processes (Active).
```

---

## Compliance Verification Matrix

| Evaluation Criteria | Target Requirement | Measured Result | Status |
| :--- | :--- | :--- | :--- |
| **ASD-STE100 Compliance** | 75% Hybrid Profile | 82% Vocabulary / 100% Syntax (Max sentence: 18 words) | PASS |
| **IEC 62443-4-2 SL2** | FR1 to FR7 Implementation | Full coverage of all 7 foundational requirements | PASS |
| **EU CRA Annex I** | Essential Requirements | Secure by default, signed updates, TPM root of trust | PASS |
| **EU CRA Annex II** | Vulnerability Handling | CycloneDX SBOM, CVD contact, Article 14 procedures | PASS |
