# Laboratory Evidence & Verification Repository

**Status: Structure Established — Evidence Pending Lab Execution**

This directory stores authentic technical artifacts generated during the completion of the CCNA Networking Lab exercises in Cisco Packet Tracer.

---

## 1. Evidence Directory Structure

```text
evidence/
├── README.md               # Evidence policies, naming conventions, and integrity standards
├── screenshots/            # Topology screenshots, ping outputs, verification displays
│   └── .gitkeep
├── configs/                # Sanitized running configurations captured post-lab
│   └── .gitkeep
└── logs/                   # Raw command outputs, verification tables, troubleshooting logs
    └── .gitkeep
```

---

## 2. File Naming Standard

Artifacts must follow a standardized naming convention mapped directly to the lab sequence:

* **Screenshots:**
  * `01-topology-initial-switching.png`
  * `02-vlan-trunk-verification.png`
  * `03-roas-routing-table.png`
  * `04-dhcp-lease-binding.png`
  * `05-fault-01-before-after.png`
  * `06-port-security-violation.png`
* **Configuration Files:**
  * `SW1-baseline-sanitized.txt`
  * `SW1-security-hardened-sanitized.txt`
  * `R1-baseline-sanitized.txt`
* **Verification Logs:**
  * `02-vlan-brief.log`
  * `02-interfaces-trunk.log`
  * `03-ip-route.log`
  * `04-dhcp-bindings.log`
  * `ping-matrix-verification.log`

---

## 3. Data Sanitization & Authenticity Standard

1. **Zero Credential Exposure:** Passwords, enable secrets, RSA private keys, or personal tokens must be redacted or sanitized prior to committing.
2. **Authenticity Guarantee:** No placeholder logs or simulated terminal captures may be committed as "proof." Artifacts are uploaded strictly after personal execution in Cisco Packet Tracer.
