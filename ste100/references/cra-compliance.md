# EU Cyber Resilience Act (CRA) Compliance Reference

The European Cyber Resilience Act (CRA - Regulation (EU) 2024/2847) establishes mandatory cybersecurity requirements for **Products with Digital Elements (PDE)** placed on the European Union single market throughout their entire lifecycle.

---

## 1. CRA Scope and Classification

| Product Category | Definition & Examples | Conformity Assessment Route |
| :--- | :--- | :--- |
| **Standard Products (Default)** | Products with digital elements that do not fall under Important or Critical categories (e.g., smart sensors, generic connected equipment). | Module A (Internal control / Self-assessment) using harmonized standards. |
| **Important Class I** | Operating systems for industrial devices, password managers, network management systems, network interfaces, microcontrollers with security features. | Harmonized standards application (Module A) OR third-party assessment (Module B+C). |
| **Important Class II** | Firewalls, industrial automation and control systems (IACS per IEC 62443), hypervisors, secure cryptoprocessors. | Mandatory third-party conformity assessment (Module B+C) or certified European cybersecurity scheme. |
| **Critical Products** | Hardware devices with security boxes, smart meter gateways. | Mandatory European cybersecurity certificate (EUCC) or specialized third-party evaluation. |

---

## 2. Essential Cybersecurity Requirements (Annex I)

### Part I: Security Requirements for Product Properties
1. **Security by Design and by Default**:
   - Products must be delivered in a secure configuration without known exploitable vulnerabilities.
   - Default passwords must not exist; every unit must enforce a unique random password or prompt for credential setup during initial commissioning.
   - Unused physical ports, network services, and debug interfaces (e.g., JTAG, Telnet) must be disabled by default.
2. **Access Control & Authentication**:
   - Prevent unauthorized access through robust authentication mechanisms (aligned with IEC 62443 SL2 FR1 & FR2).
3. **Data Confidentiality & Integrity**:
   - Encrypt sensitive data in transit and at rest using modern, tested cryptographic algorithms.
4. **Attack Surface Minimization**:
   - Restrict code execution, prevent buffer overflows, and minimize privileges required for software execution.
5. **Secure Software Updates**:
   - Enable secure delivery and automatic/assisted application of security patches.
   - Separate security updates from feature updates so users can apply security fixes without operational risk.
   - Verify digital signatures on update packages prior to execution.

### Part II: Vulnerability Handling Requirements
1. **Coordinated Vulnerability Disclosure (CVD)**:
   - Establish and publish a CVD policy.
   - Provide a public contact point for security researchers (e.g., `security@company.com` and a `/.well-known/security.txt` file).
2. **Software Bill of Materials (SBOM)**:
   - Maintain a complete, machine-readable Software Bill of Materials (SBOM) in an industry-standard format:
     - **CycloneDX** (JSON/XML) or **SPDX** (JSON/Tag-Value).
   - The SBOM must inventory:
     - Component names, versions, supplier/author.
     - Direct and transitive dependencies.
     - Cryptographic hashes of binaries.
     - License information and known vulnerability tracking (CVE IDs).
3. **Continuous Vulnerability Remediation**:
   - Regularly monitor vulnerability databases (NVD, GitHub Advisory Database) for newly discovered CVEs.
   - Release security patches without delay and free of charge.
4. **Support Period Commitment**:
   - Clearly state the guaranteed security support period upfront (minimum 5 years or the expected product lifetime).

---

## 3. Mandatory Reporting Timelines (Article 14)

Manufacturers must notify the designated **national CSIRT** (Computer Security Incident Response Team) and **ENISA** (European Union Agency for Cybersecurity) of any actively exploited vulnerability or severe security incident:

```
┌─────────────────┐       ┌─────────────────┐       ┌─────────────────┐
│  Early Warning  │ ────► │  Notification   │ ────► │  Final Report   │
│   Within 24h    │       │   Within 72h    │       │  Within 1 Month │
└─────────────────┘       └─────────────────┘       └─────────────────┘
```

### 1. Early Warning (Within 24 Hours)
- **Trigger**: Becoming aware of an actively exploited vulnerability or a severe incident affecting product security.
- **Content**:
  - Initial notification that an incident or exploited vulnerability has occurred.
  - Indication whether the incident is suspected of having malicious intent or cross-border impact.

### 2. Incident / Vulnerability Notification (Within 72 Hours)
- **Content**:
  - Detailed description of the vulnerability or incident.
  - Initial assessment of severity, affected product versions, and scope of impact.
  - Any mitigation measures already implemented or advised to end users.

### 3. Final Report (Within 1 Month)
- **Content**:
  - Comprehensive root-cause analysis.
  - Full description of the exploit mechanism and attack vector.
  - Final remediation patch details and instructions for users.
  - Corrective actions to prevent future recurrences in the product lifecycle.

---

## 4. Technical Documentation Requirements (Annex VII)

To achieve CE marking and demonstrate compliance, the technical documentation dossier must include:
1. Complete product description and architecture diagram.
2. Cybersecurity risk assessment covering potential threats and attack vectors.
3. Mapping of applied standards (IEC 62443-4-1, IEC 62443-4-2, IEC 62443-3-3).
4. Machine-readable SBOM file (CycloneDX / SPDX).
5. Coordinated vulnerability disclosure and incident management policy.
6. User cybersecurity instructions (written in clear ASD-STE100).
7. Test reports and cryptographic validation records.
