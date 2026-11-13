# IEC 62443 Security Level 2 (SL2) Technical Guidelines

IEC 62443 is the global benchmark standard for the cybersecurity of Industrial Automation and Control Systems (IACS). This guide defines technical specifications and documentation rules for achieving and demonstrating **Security Level 2 (SL 2)**.

---

## 1. Security Level 2 (SL2) Threat Profile

| Parameter | Specification |
| :--- | :--- |
| **Definition** | Protection against intentional violation using simple means with low resources, generic skills, and low motivation. |
| **Typical Adversary** | Script kiddies, opportunistic attackers using public exploit tools, disgruntled insiders with standard operational access. |
| **Attack Vectors** | Default credential exploitation, unencrypted traffic sniffing, replay attacks, public known vulnerabilities (unpatched CVEs), network scanning. |
| **Core Defense Strategy** | Strong authentication, role-based access control, zone/conduit boundary filtering, encryption of sensitive data in transit, cryptographic firmware signing, and tamper-resistant audit logging. |

---

## 2. Foundational Requirements (FRs) for SL2

The standard defines 7 Foundational Requirements (IEC 62443-3-3 for systems, IEC 62443-4-2 for components):

### FR 1: Identification & Authentication Control (IAC)
- **Unique Identification (SR 1.1 / CR 1.1)**: Every human user and system service must have a unique identifier. Shared or generic accounts (e.g., `admin`, `operator`) are prohibited.
- **Multifactor Authentication (SR 1.2 / CR 1.2)**: Required for all remote access and access originating from untrusted zones (e.g., corporate IT or Internet).
- **Password Strength & Complexity (SR 1.5 / CR 1.5)**:
  - Minimum 12 characters.
  - Must include uppercase, lowercase, digits, and special characters.
  - Passwords must be hashed using strong one-way cryptographic algorithms with salt (e.g., PBKDF2, bcrypt, Argon2).
- **Account Lockout (SR 1.11 / CR 1.11)**:
  - System must lock the account after a maximum of 5 consecutive failed login attempts.
  - Lockout duration: Minimum 15 minutes or manual unlock by an administrator.
- **Session Timeout (SR 1.13 / CR 1.13)**:
  - Automatic session lockout after a maximum of 15 minutes of inactivity for interactive user interfaces.

### FR 2: Use Control (UC)
- **Role-Based Access Control - RBAC (SR 2.1 / CR 2.1)**:
  - Enforce least privilege based on predefined roles:
    1. **Operator**: Read-only monitoring, setpoint adjustments within restricted limits.
    2. **Maintenance**: Diagnostics, error log retrieval, calibration.
    3. **Engineer**: Logic modification, recipe updates, communication configuration.
    4. **Security Administrator**: User management, certificate renewal, security audit log access.
- **Concurrent Session Limits (SR 2.8 / CR 2.8)**:
  - Limit simultaneous active sessions per user account to prevent credential sharing and session hijacking.
- **Audit Account Creation & Deletion (SR 2.2 / CR 2.2)**:
  - All privilege elevation, account provisioning, and role assignment actions must be recorded in the audit log.

### FR 3: System Integrity (SI)
- **Firmware & Software Authenticity (SR 3.4 / CR 3.4)**:
  - The system must verify the cryptographic digital signature of firmware and software updates before installation (e.g., RSA-3072 or ECDSA P-256 with SHA-256).
  - Unsigned or invalidly signed updates must be rejected and logged as a security alert.
- **Secure Boot (CR 3.14)**:
  - Hardware root of trust validates the initial bootloader and operating system kernel prior to execution.
- **Configuration Integrity (SR 3.1 / CR 3.1)**:
  - Detect unauthorized modifications to critical configuration files using cryptographic checksums (SHA-256) or file integrity monitoring (FIM).

### FR 4: Data Confidentiality (DC)
- **Data in Transit (SR 4.1 / CR 4.1)**:
  - Encrypt all sensitive communications across zone boundaries using approved TLS 1.3 or IPsec tunnels.
  - Minimum ciphersuite: `TLS_AES_128_GCM_SHA256` or equivalent.
  - Legacy plaintext protocols (Telnet, HTTP, unauthenticated FTP, unencrypted Modbus/TCP across conduits) must be disabled.
- **Data at Rest (SR 4.2 / CR 4.2)**:
  - Protect cryptographic private keys, passphrases, and sensitive configuration data using AES-128/256 or hardware-protected keystores (TPM / Secure Element).

### FR 5: Restricted Data Flow (RDF)
- **Zone and Conduit Architecture (SR 5.1 / CR 5.1)**:
  - Partition the network into logical zones based on criticality per IEC 62443-3-2:
    - **Zone 0 / 1**: Field devices, PLCs, safety controllers, sensors, actuators.
    - **Zone 2**: Supervisory SCADA, engineering workstations, local HMIs.
    - **Zone 3**: Operations management, MES, industrial historians.
    - **Zone 4**: Corporate IT network (Enterprise).
  - All communication between zones must pass through defined conduits protected by industrial firewalls or deep packet inspection (DPI) proxies.
- **Default-Deny Policy (SR 5.2 / CR 5.2)**:
  - Block all traffic through conduits by default. Explicitly permit only necessary IP addresses, ports, and protocols.

### FR 6: Timely Response to Events (TRE)
- **Security Audit Logging (SR 6.1 / CR 6.1)**:
  - Log all security-relevant events:
    - Successful and failed authentication attempts.
    - User account creation, modification, and deletion.
    - Configuration and parameter changes.
    - Firmware update attempts.
    - Communication errors and conduit boundary firewall drops.
- **Log Protection (SR 6.2 / CR 6.2)**:
  - Prevent unauthorized modification or deletion of audit logs.
  - Forward logs in real time to a centralized syslog server over TLS (RFC 5424 / RFC 5425).
- **Time Synchronization (SR 6.1 / CR 6.1)**:
  - Synchronize internal clocks with an authenticated NTP (Network Time Protocol) server to ensure valid audit event ordering.

### FR 7: Resource Availability (RA)
- **Denial of Service (DoS) Mitigation (SR 7.1 / CR 7.1)**:
  - Implement network rate limiting, TCP SYN cookies, and queue management to resist packet flooding attacks.
- **Deterministic Watchdog & Fail-Safe State (SR 7.2 / CR 7.2)**:
  - Provide hardware/software watchdogs to detect application hangs and revert the system to a predefined safe state.
- **Backup & Disaster Recovery (SR 7.3 / CR 7.3)**:
  - Document and test automated procedures for system configuration backup and bare-metal recovery within defined RTO (Recovery Time Objective) parameters.

---

## 3. IEC 62443 SL2 Verification Checklist

```
[ ] FR1: Unique user accounts enforced (no generic passwords).
[ ] FR1: Password minimum length ≥ 12 with complexity checks.
[ ] FR1: Account lockout active (max 5 failed attempts, 15 min lock).
[ ] FR1: Inactivity timeout active (15 minutes).
[ ] FR2: Role-based access control (RBAC) configured and tested.
[ ] FR3: Digital signature verification on all software/firmware updates.
[ ] FR3: Secure boot hardware root-of-trust verified.
[ ] FR4: TLS 1.3 / AES-128 encryption on all inter-zone communication.
[ ] FR5: Network segmented into zones and conduits; firewall default-deny.
[ ] FR6: Audit logs forward to centralized syslog over TLS with NTP sync.
[ ] FR7: DoS rate limiting enabled; backup and restore verified.
```
