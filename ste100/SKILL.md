---
name: ste100
description: Author, review, or refactor technical documentation, security specifications, and operational manuals according to ASD-STE100 (Simplified Technical English), IEC 62443 SL2 (Security Level 2), and the EU Cyber Resilience Act (CRA). Triggers on requests involving technical authoring, cybersecurity compliance, industrial automation documentation, SBOM and vulnerability policies, or CRA technical files. Prompts the user to specify the ASD-STE100 application percentage before generating content.
---

# ASD-STE100 Technical Authoring with IEC 62443 SL2 & EU CRA

This skill directs the creation, refactoring, and auditing of technical and security documentation under three unified standards:
1. **ASD-STE100 (Issue 8)**: Controlled language reducing ambiguity and cognitive load.
2. **IEC 62443 SL2**: Industrial Automation and Control Systems (IACS) Security Level 2 requirements.
3. **EU Cyber Resilience Act (CRA - Regulation 2024/2847)**: Mandatory product cybersecurity, SBOM, and lifecycle vulnerability handling.

---

## Execution Workflow

Follow this 5-step procedure on every invocation:

```
[Step 1: Ask ASD-STE100 %] ──► [Step 2: Classify Target Doc] ──► [Step 3: Apply Standards] ──► [Step 4: Quality Gate] ──► [Step 5: Compliance Summary]
```

---

### Step 1: Prompt User for ASD-STE100 Application Percentage

> [!IMPORTANT]
> **Mandatory First Action**: You must verify or request the percentage of ASD-STE100 compliance before generating or refactoring documentation.

If the user has not explicitly stated the target percentage in their prompt, ask them immediately:

> *"Please specify the target percentage of ASD-STE100 application for this document:*
> * 1. **100% (Strict ASD-STE100)**: Full dictionary constraint. Only approved words and parts of speech. Max 20 words for instructions, max 25 words for descriptions. Zero unapproved synonyms.
> * 2. **75% - 80% (Hybrid / Technical Domain - Recommended)**: Full ASD-STE100 grammar and syntax (active voice, short sentences, 1 instruction/sentence, imperative steps, noun clusters ≤ 3), but allows normative domain terminology from IEC 62443 and CRA (e.g., 'authentication', 'cryptographic', 'vulnerability', 'conduit', 'SBOM') without artificial rephrasing.
> * 3. **50% (Core Clarity Profile)**: Core simplified English principles (short sentences, active voice, vertical lists) with free domain vocabulary.
> * 4. **Custom %**: User-specified custom percentage or custom rules.*"

Adapt the enforcement level based on the selected percentage:
- Consult [ste100-rules.md](./references/ste100-rules.md#percentage-profiles) for exact constraints per level.

---

### Step 2: Classify Target Document & Scope

Determine the document type and applicable standard sections:

| Document Type | Primary Standards | Key Artifacts / Outputs |
| :--- | :--- | :--- |
| **Security Manual / Operator Guide** | ASD-STE100 + IEC 62443-3-3 / 4-2 | Step-by-step procedures, role definitions, access control |
| **CRA Technical Dossier** | ASD-STE100 + CRA Annex I & VII | Product description, risk assessment, cybersecurity design |
| **SBOM & Vulnerability Policy** | CRA Annex I Part II + IEC 62443-4-1 | CVD process, machine-readable SBOM format, patch SLA |
| **Zone & Conduit Architecture** | IEC 62443-3-2 / 3-3 SL2 | Boundary definition, conduit filtering, protocol whitelist |
| **Incident Response Protocol** | CRA Article 14 + IEC 62443-2-4 | 24h early warning, 72h incident notification, ENISA/CSIRT |

---

### Step 3: Apply Combined Directives

When writing content, strictly apply the rules from the reference documents:

#### A. ASD-STE100 Writing Rules
Refer to [ste100-rules.md](./references/ste100-rules.md):
- **Sentence Length**: Maximum 20 words for procedural steps; maximum 25 words for descriptions.
- **Single Instruction**: One command per procedural sentence.
- **Voice & Mood**: Active voice only. Imperative mood for procedural steps (`Start the engine.`, not `The engine must be started.`).
- **Noun Clusters**: Maximum 3 consecutive nouns. Unpack clusters with prepositions (e.g., `user account lockout counter` ➔ `counter for user account lockouts`).
- **Approved Words**: Use only approved words for the selected percentage profile. Avoid prohibited synonyms (`make sure` ➔ `ensure` / `verify`; `shut down` ➔ `stop`).

#### B. IEC 62443 Security Level 2 (SL2) Rules
Refer to [iec62443-sl2-guidelines.md](./references/iec62443-sl2-guidelines.md):
- Target threat: Protection against intentional violation using simple means with low resources, generic skills, low motivation.
- Ensure all 7 Foundational Requirements (FR1 to FR7) are satisfied at SL2:
  - **FR1 (IAC)**: Unique user accounts, password complexity, lockout after failed attempts (max 5), session timeout (15 min), MFA for untrusted/remote access.
  - **FR2 (UC)**: RBAC (Operator, Maintenance, Engineer, Admin), least privilege, session limits.
  - **FR3 (SI)**: Cryptographic signature on firmware updates, Secure Boot, software integrity check.
  - **FR4 (DC)**: Data in transit encrypted via TLS 1.3 / AES-128 minimum; sensitive data at rest protected.
  - **FR5 (RDF)**: Zones and conduits defined; firewalls enforce default-deny across conduits.
  - **FR6 (TRE)**: Centralized audit logging (syslog over TLS); authenticated NTP time source; audit log protection.
  - **FR7 (RA)**: DoS mitigation, rate limiting, deterministic watchdog restart, backup and restore procedures.

#### C. EU Cyber Resilience Act (CRA) Rules
Refer to [cra-compliance.md](./references/cra-compliance.md):
- **Security by Design & Default**: Products shipped with secure defaults (no default blank/hardcoded passwords, disabled unnecessary ports and protocols).
- **Vulnerability Handling**: Coordinated Vulnerability Disclosure (CVD), public security contact (`security.txt`), guaranteed free security updates for minimum 5 years.
- **SBOM**: Machine-readable Software Bill of Materials (CycloneDX / SPDX) tracking all components and dependencies.
- **Mandatory Reporting Timelines (Article 14)**:
  - **24 hours**: Early warning to CSIRT / ENISA of actively exploited vulnerability or severe incident.
  - **72 hours**: Full notification with initial findings.
  - **1 month**: Final report with root-cause analysis and remediation.

---

### Step 4: Quality Gate & Verification

Before finalizing output, verify against these checkable criteria:

```
[ ] ASD-STE100 Check:
    - Are instructions ≤ 20 words?
    - Are descriptions ≤ 25 words?
    - Are all procedures in active voice and imperative mood?
    - Are noun clusters ≤ 3 nouns?
    - Does vocabulary conform to the requested percentage profile?

[ ] IEC 62443 SL2 Check:
    - Are relevant FRs (FR1 - FR7) explicitly addressed?
    - Are authentication, session timeouts, and RBAC specified?
    - Are encryption, network segmentation, and logging mechanisms defined?

[ ] CRA Check:
    - Are security-by-default configurations documented?
    - Is SBOM generation / maintenance specified?
    - Are vulnerability handling and reporting deadlines (24h/72h/1m) integrated?
```

---

### Step 5: Compliance Summary Matrix

Always append a concise compliance table at the end of generated or reviewed documents:

```markdown
## Compliance Verification Matrix

| Standard | Target Level | Achieved Compliance | Notes / Observations |
| :--- | :--- | :--- | :--- |
| **ASD-STE100** | [Selected %] | [Calculated / Verified %] | [Average sentence length, vocabulary compliance] |
| **IEC 62443** | SL2 | Compliant | [FR1-FR7 coverage summary] |
| **EU CRA** | Essential Req. (Annex I) | Compliant | [SBOM, CVD, Secure Update, 24h/72h Reporting] |
```

---

## Detailed References & Templates

- [ste100-rules.md](./references/ste100-rules.md): Full ASD-STE100 grammar, vocabulary, and percentage guidelines.
- [iec62443-sl2-guidelines.md](./references/iec62443-sl2-guidelines.md): Technical controls for IEC 62443-3-3 & 4-2 SL2.
- [cra-compliance.md](./references/cra-compliance.md): Cyber Resilience Act essential requirements and timeline checklists.
- [security-procedure-ste100.md](./templates/security-procedure-ste100.md): Template for operational security procedures in STE100.
- [cra-technical-dossier-ste100.md](./templates/cra-technical-dossier-ste100.md): Template for CRA technical documentation dossiers.
