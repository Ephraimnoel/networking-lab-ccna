# Switch & Device Security Baseline

**Status: Security Specification & Hardening Standard (Design Baseline)**  
*Applies to: Cisco Catalyst 2960 (`Northstar-SW1`) and Cisco Router (`Northstar-R1`)*

---

## 1. Objective

This standard defines the foundational Layer 2 switch security and management plane hardening controls for Northstar Services. These controls mitigate common local network vulnerabilities including MAC flooding, unauthorized device attachment, rogue trunk negotiation (DTP abuse), and insecure plaintext management.

---

## 2. Layer 2 Switch Hardening Standards

### Control 2.1: Parking & Disabling Unused Switchports
* **Vulnerability:** An unauthorized visitor or insider connects a rogue laptop to an empty wall-jack or patch panel, gaining immediate network access.
* **Hardening Standard:** All unused physical interfaces must be administratively shut down and assigned to an unrouted blackhole VLAN (VLAN 999).
* **Configuration Syntax:**
  ```cisco
  interface range FastEthernet0/16 - 24, GigabitEthernet0/1 - 2
   description UNUSED_PORT_PARKED
   switchport mode access
   switchport access vlan 999
   shutdown
  ```

### Control 2.2: Port Security (MAC Address Limiting)
* **Vulnerability:** MAC Address Flooding (filling the switch CAM table to force fail-open hub behavior) and unauthorized hub/switch attachment.
* **Hardening Standard:** Enable port security on all active access ports, limit maximum allowed MACs to 2 (allowing PC + IP phone or laptop swap), learn addresses dynamically via sticky learning, and set violation mode to `restrict` (drops packets from unauthorized MACs and increments security counter without shutting down the entire port).
* **Configuration Syntax:**
  ```cisco
  interface range FastEthernet0/2 - 15
   switchport mode access
   switchport port-security
   switchport port-security maximum 2
   switchport port-security violation restrict
   switchport port-security mac-address sticky
  ```

### Control 2.3: Trunk Hardening & DTP Elimination
* **Vulnerability:** VLAN Hopping via Switch Spoofing (an endpoint pretending to be a switch to form a trunk link via Dynamic Trunking Protocol).
* **Hardening Standard:** Disable DTP on all access ports with `switchport nonegotiate`. On trunk ports, explicitly prune allowed VLANs and reassign the native VLAN away from default VLAN 1.
* **Configuration Syntax:**
  ```cisco
  ! On Access Interfaces:
  interface range FastEthernet0/2 - 15
   switchport nonegotiate

  ! On Trunk Interface:
  interface FastEthernet0/1
   switchport mode trunk
   switchport trunk native vlan 99
   switchport trunk allowed vlan 10,20,30,99
   switchport nonegotiate
  ```

---

## 3. Management Plane & Access Hardening

### Control 3.1: Enforce Secure Management (SSHv2 over Telnet)
* **Vulnerability:** Telnet transmits administrative credentials and configuration data in cleartext across the network.
* **Hardening Standard:** Disable Telnet globally on all virtual terminal lines (`line vty`); mandate SSH version 2 using 2048-bit RSA keys.
* **Configuration Syntax:**
  ```cisco
  ip domain-name northstar.local
  crypto key generate rsa modulus 2048
  ip ssh version 2
  ip ssh time-out 60
  ip ssh authentication-retries 2

  line vty 0 4
   transport input ssh
   login local
   exec-timeout 5 0
  ```

### Control 3.2: Local Authentication & Password Hashing
* **Vulnerability:** Plaintext passwords in configuration files or weak hashing algorithms (Type 7).
* **Hardening Standard:** Use strong secret hashing (`enable secret`) and obscure cleartext passwords with `service password-encryption`. Configure named local administrative accounts rather than shared line passwords.
* **Configuration Syntax:**
  ```cisco
  service password-encryption
  username admin privilege 15 secret [LAB_ADMIN_SECRET]
  enable secret [LAB_ENABLE_SECRET]

  line con 0
   login local
   exec-timeout 5 0
   logging synchronous
  ```
  *(Note: Actual secrets are sanitized and omitted from public repository documentation).*

### Control 3.3: Warning Banners (Legal Notice)
* **Hardening Standard:** Configure a Message of the Day (MOTD) banner warning that unauthorized access is prohibited and monitored.
* **Configuration Syntax:**
  ```cisco
  banner motd #
  =============================================================
  [!] NORTHSTAR SERVICES — RESTRICTED ACCESS ONLY
  Unauthorized access or usage is strictly prohibited.
  All network activities are logged and monitored.
  =============================================================
  #
  ```

---

## 4. Planned Boundary Filtering (Access Control Lists)

In subsequent lab phases, standard and extended IPv4 Access Control Lists (ACLs) will be applied at the Layer 3 router (`Northstar-R1`):
1. **Financial Network Isolation (VLAN 20):** Restrict general Administration hosts (VLAN 10) from initiating direct TCP/IP connections to Finance endpoints, permitting only authorized transactional ports.
2. **Administrative SVI Protection:** Restrict incoming SSH connections to the switch SVI (`10.10.99.2`) exclusively from the IT subnet (`10.10.30.0/27`).
