# ASD-STE100 (Simplified Technical English) Rules & Guidelines

ASD-STE100 is an international specification for the preparation of technical documentation in a controlled language. It simplifies text, reduces ambiguity, and standardizes vocabulary to improve clarity for readers worldwide.

---

## 1. Percentage Profiles

When the user specifies an ASD-STE100 percentage, apply the corresponding profile:

| Profile | Target % | Vocabulary Constraint | Sentence Length | Grammar & Voice | Best For |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Strict STE** | **100%** | Official ASD-STE100 dictionary only. Zero unapproved synonyms. | Max 20 words (procedural)<br>Max 25 words (descriptive) | Active voice only. Imperative for steps. Noun clusters ≤ 3. Zero gerunds in modifiers. | Formal aerospace, defense manuals, strict compliance audits. |
| **Hybrid / Engineering** *(Recommended)* | **75% - 80%** | ASD-STE100 dictionary + recognized normative domain terms (IEC 62443, CRA, cryptography, networking). | Max 20 words (procedural)<br>Max 25 words (descriptive) | Active voice only. Imperative for steps. Noun clusters ≤ 3. One instruction per sentence. | Industrial cybersecurity documentation, technical compliance dossiers, software guides. |
| **Core Clarity** | **50%** | Free technical vocabulary. Avoid unnecessary jargon. | Max 25 words per sentence | Active voice prioritized. Imperative for steps. Clear vertical lists. | Developer readmes, internal wikis, quick reference notes. |
| **Custom** | User % | Interpolated based on user constraints. | Adapted to user request | Follow core structure | Specialized projects. |

---

## 2. Core Sentence Rules

### Rule 2.1: Sentence Length
- **Procedural sentences** (instructions, action steps): **Maximum 20 words**.
- **Descriptive sentences** (explanations, context, descriptions): **Maximum 25 words**.
- Keep sentences short. One thought per sentence.

*Incorrect:*
> The operator must make sure that all the cables are connected securely to the main power unit and check that the green status LED is on before the power switch is set to the ON position. (35 words)

*Correct:*
> Make sure that all cables connect to the power unit. (10 words)
> Verify that the green status LED is on. (8 words)
> Set the power switch to the ON position. (8 words)

### Rule 2.2: One Instruction per Sentence
- Do not combine two separate actions into one sentence with conjunctions like "and" or "then".

*Incorrect:*
> Remove the protective cover and loosen the two retaining screws.

*Correct:*
> 1. Remove the protective cover.
> 2. Loosen the two retaining screws.

### Rule 2.3: Active Voice & Imperative Mood
- Use active voice. Identify who performs the action.
- For procedural steps, always use the **imperative mood** (the base form of the verb without "you" or "must").

*Incorrect (Passive):*
> The certificate must be imported into the keystore by the security engineer.

*Correct (Active - Descriptive):*
> The security engineer imports the certificate into the keystore.

*Correct (Imperative - Procedure):*
> Import the certificate into the keystore.

### Rule 2.4: Noun Clusters (Maximum 3 Nouns)
- Do not chain more than 3 consecutive nouns.
- Unpack clusters using prepositions (e.g., *of*, *for*, *in*).

| Non-Compliant (Noun Cluster > 3) | Compliant ASD-STE100 |
| :--- | :--- |
| `industrial firewall zone boundary rule set` | `rule set for the industrial firewall zone boundary` |
| `firmware update signature verification algorithm` | `algorithm for firmware update signature verification` |
| `user session inactivity timeout configuration parameter` | `parameter for user session inactivity timeout` |

### Rule 2.5: Verb Forms and Gerunds
- Avoid gerunds (`-ing`) when they function as adjectives or verbal nouns if they create ambiguity.
- Use simple past tense, simple present tense, or imperative.

*Incorrect:*
> While operating the system, avoiding connecting unauthorized USB devices is recommended.

*Correct:*
> Do not connect unauthorized USB devices during system operation.

---

## 3. Vocabulary & Approved Words Reference

### Common Verbs: Approved vs. Unapproved

| Do Not Use (Unapproved) | Use Instead (Approved ASD-STE100) | Notes |
| :--- | :--- | :--- |
| `abort` / `terminate` / `halt` | `stop` / `cancel` | Standardize on `stop` for operations and `cancel` for procedures. |
| `activate` / `initiate` / `trigger` | `start` / `energize` | Use `start` for processes/programs. Use `energize` for electrical circuits. |
| `allow` / `permit` | `let` / `permit` (if noun) | In STE: Use `let` or rephrase with `can`. |
| `ascertain` / `check out` | `examine` / `verify` / `test` | Be specific about what action is performed. |
| `commence` / `launch` | `start` | Always use `start`. |
| `configure` | `set` / `configure` *(domain term at 75%)* | In strict STE, use `set` or `adjust`. |
| `depress` | `push` / `press` | Use `push` for buttons or switches. |
| `display` / `indicate` | `show` | Use `show` for screens, meters, and status lights. |
| `ensure` / `make sure` | `make sure` *(Strict STE)* / `ensure` *(75% Domain)* | ASD-STE100 approves `make sure that`. |
| `execute` | `run` / `do` | Use `run` for scripts and programs. |
| `illuminate` | `come on` / `turn on` | Example: `The red LED comes on.` |
| `modify` / `alter` | `change` | Always use `change`. |
| `monitor` | `monitor` *(approved noun/verb in context)* | Check periodically. |
| `obtain` | `get` | Always use `get`. |
| `shut down` / `turn off` | `stop` / `de-energize` | Use `stop` for software, `de-energize` for electrical power. |
| `utilize` / `employ` | `use` | Always use `use`. |

### Technical Words in IEC 62443 / CRA Context (75% Profile)

When using the **75% - 80% Hybrid Profile**, the following technical and normative terms are permitted as technical names without dictionary substitution:

- **Security & Crypto**: `authentication`, `authorization`, `cryptographic`, `hash`, `tamper-evident`, `keystore`, `certificate`, `signature`, `entropy`, `ciphersuite`, `encryption`, `decryption`.
- **Architecture & Network**: `zone`, `conduit`, `firewall`, `VLAN`, `DMZ`, `gateway`, `endpoint`, `packet filter`.
- **CRA & Regulatory**: `SBOM` (Software Bill of Materials), `vulnerability`, `CVE`, `CVD` (Coordinated Vulnerability Disclosure), `CSIRT`, `ENISA`, `patch`, `mitigation`, `incident`, `conformity assessment`.

---

## 4. Warnings, Cautions, and Notes

ASD-STE100 strictly defines safety and operational notices:

### WARNING (Risk of injury or death)
```markdown
> [!WARNING]
> HIGH VOLTAGE HAZARD.
> DISCONNECT THE MAIN POWER SUPPLY BEFORE YOU OPEN THE CABINET.
```

### CAUTION (Risk of equipment damage, security breach, or data loss)
```markdown
> [!CAUTION]
> SECURITY BREACH RISK.
> DO NOT TRANSMIT ENCRYPTION KEYS OVER UNENCRYPTED CHANNELS.
```

### NOTE (Important technical context)
```markdown
> [!NOTE]
> The default session timeout is 15 minutes.
```
