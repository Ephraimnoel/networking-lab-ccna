# Lab 06 — Foundational Device & Switchport Security

**Status: Planned / Simulation Ready**  
*Simulator: Cisco Packet Tracer*

---

## 1. Objective
Implement the hardening baseline defined in [`docs/security-baseline.md`](../docs/security-baseline.md) across `Northstar-SW1` and `Northstar-R1`, covering unused switchport parking, MAC-based port security, secure management (SSHv2), and line protections.

## 2. Prerequisites
* Labs 01–04 completed and verified.
* Security baseline reviewed ([`docs/security-baseline.md`](../docs/security-baseline.md)).

## 3. Guided Implementation Tasks

### Task 3.1: Switchport Hardening & Unused Port Parking
On `Northstar-SW1`:
```cisco
enable
configure terminal

! Park and Disable All Unused Switchports
interface range FastEthernet0/16 - 24, GigabitEthernet0/1 - 2
 description PARKING_BLACKHOLE_VLAN999
 switchport mode access
 switchport access vlan 999
 shutdown
exit
```

### Task 3.2: Configure Port Security on User Access Ports
```cisco
interface range FastEthernet0/2 - 15
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
exit
```

### Task 3.3: Secure Management Plane Hardening (SSHv2 & Local Auth)
```cisco
! Global Management Hardening
service password-encryption
ip domain-name northstar.local
crypto key generate rsa modulus 2048
ip ssh version 2
ip ssh time-out 60
ip ssh authentication-retries 2

username admin privilege 15 secret LabAdminSecret123!
enable secret LabEnableSecret123!

! VTY Line Security
line vty 0 4
 transport input ssh
 login local
 exec-timeout 5 0
exit

! Console Hardening
line con 0
 login local
 exec-timeout 5 0
 logging synchronous
exit

! Legal MOTD Banner
banner motd #
=============================================================
RESTRICTED NETWORK ASSET — AUTHORIZED PERSONNEL ONLY
All activities are logged and monitored.
=============================================================
#
```

## 4. Expected Outcomes & Verification
1. `show port-security` confirms port security is active across `Fa0/2 - Fa0/15`.
2. `show port-security interface Fa0/2` shows sticky MAC learning and violation mode `Restrict`.
3. `show ip ssh` confirms SSH version 2 is enabled.
4. Telnet connection attempt to switch SVI `10.10.99.2` is rejected.
5. SSH connection from endpoint terminal to `10.10.99.2` connects and prompts for local credentials.

## 5. Required Evidence Artifacts
* Command text output: `show port-security`.
* Command text output: `show ip ssh`.
* Terminal session log: Verification of rejected Telnet and accepted SSH session.
