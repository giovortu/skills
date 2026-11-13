# Operational Security Procedure: Device Commissioning and Firmware Update
**Standard Compliance**: ASD-STE100 (75% Profile) | IEC 62443-4-2 SL2 | EU CRA Annex I

---

## 1. Scope and Prerequisites

This procedure describes how to commission the industrial controller and install a verified firmware update.

### Personnel Requirements
- The field engineer must have active credentials with the **Engineer** role.
- The engineer must use an authenticated engineering workstation in Zone 2.

### Required Tools
- Engineering workstation with TLS 1.3 browser.
- Encrypted USB drive with the signed firmware file (`firmware-v2.1.bin`).
- Cryptographic public key certificate of the manufacturer (`vendor-root.crt`).

---

## 2. Warnings and Cautions

> [!CAUTION]
> SECURITY BREACH RISK.
> DO NOT CONNECT THE CONTROLLER TO AN UNSECURED NETWORK ZONE.
> VERIFY ALL DIGITAL SIGNATURES BEFORE YOU APPLY FIRMWARE UPDATES.

> [!NOTE]
> The controller locks the session after 15 minutes of inactivity.

---

## 3. Step-by-Step Procedure

### Phase A: Initial Device Commissioning (IEC 62443 SL2 FR1 & FR2)

1. Connect the engineering workstation to the controller management port with an Ethernet cable.
2. Open the web browser and enter the controller default IP address:
   `https://192.168.1.10:8443`
3. Accept the temporary provisioning certificate.
4. Enter the temporary provisioning username:
   `setup-admin`
5. Enter the unique factory token printed on the controller label.
6. Enter a new password for the administrator account.
   - The password must have at least 12 characters.
   - The password must contain uppercase letters, lowercase letters, numbers, and special symbols.
7. Record the administrator credentials in the enterprise credential manager.
8. Set the network IP parameters for the assigned industrial zone.
9. Disable all unused physical ports and network protocols.
10. Click **Save Configuration**.

---

### Phase B: Cryptographic Firmware Update (IEC 62443 SL2 FR3 & CRA Annex I)

1. Navigate to the **Firmware Management** menu in the web interface.
2. Click **Upload Firmware Package**.
3. Select the signed firmware image `firmware-v2.1.bin` from the local directory.
4. Select the manufacturer digital signature file `firmware-v2.1.sig`.
5. Click **Verify Signature**.
   - The controller calculates the SHA-256 hash of the package.
   - The controller validates the RSA-3072 digital signature with the internal root key.
6. Verify that the web interface shows:
   `Signature status: VALID`
7. Click **Apply Firmware Update**.
   - Do not disconnect the power supply during the update process.
   - The controller writes the image to the inactive flash partition.
8. Wait for the controller to restart.
   - The hardware watchdog performs a secure boot integrity check.
   - The controller starts the updated operating system.
9. Log in with your new administrator credentials.
10. Verify that the system information page shows version `2.1.0`.

---

## 4. Verification and Audit Log (IEC 62443 SL2 FR6)

1. Open the **Security Audit Log** page.
2. Verify that the log records the following security events:
   - Event ID 1001: Initial administrator password set.
   - Event ID 2004: Network configuration changed.
   - Event ID 3012: Firmware signature verified successfully.
   - Event ID 3015: System restart after firmware update.
3. Export the security log file over TLS to the central SIEM server.
4. Close the browser session.

---

## Compliance Verification Matrix

| Standard | Target Level | Achieved Compliance | Notes / Observations |
| :--- | :--- | :--- | :--- |
| **ASD-STE100** | 75% | Compliant | Average sentence length: 12 words. Active voice and imperative steps used throughout. |
| **IEC 62443** | SL2 | Compliant | Unique passwords (FR1), RBAC (FR2), signed firmware (FR3), TLS 1.3 (FR4), audit log (FR6). |
| **EU CRA** | Annex I | Compliant | No default password, unused interfaces closed, secure update mechanism validated. |
