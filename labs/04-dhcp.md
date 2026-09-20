# Lab 04 — Dynamic Host Configuration Protocol (DHCP)

**Status: Planned / Simulation Ready**  
*Simulator: Cisco Packet Tracer*

---

## 1. Objective
Configure centralized Cisco IOS DHCP services on `Northstar-R1`, configure address exclusion ranges for infrastructure reservations, set default gateway and DNS options per scope, and verify dynamic client lease acquisition.

## 2. Prerequisites
* Lab 03 completed (routing operational).
* IP addressing plan reviewed ([`docs/ip-addressing-plan.md`](../docs/ip-addressing-plan.md)).

## 3. Guided Implementation Tasks

### Task 3.1: Configure Address Exclusions (Static IP Protection)
On `Northstar-R1`:
```cisco
enable
configure terminal

! Exclude Gateways and Static Reservations
ip dhcp excluded-address 10.10.10.1 10.10.10.9
ip dhcp excluded-address 10.10.20.1 10.10.20.4
ip dhcp excluded-address 10.10.30.1 10.10.30.9
```

### Task 3.2: Configure Departmental DHCP Pools
```cisco
! Administration Scope
ip dhcp pool ADMIN_POOL
 network 10.10.10.0 255.255.255.224
 default-router 10.10.10.1
 dns-server 1.1.1.1
exit

! Finance Scope
ip dhcp pool FINANCE_POOL
 network 10.10.20.0 255.255.255.240
 default-router 10.10.20.1
 dns-server 1.1.1.1
exit

! IT Scope
ip dhcp pool IT_POOL
 network 10.10.30.0 255.255.255.224
 default-router 10.10.30.1
 dns-server 1.1.1.1
exit
```

### Task 3.3: Client Verification & Lease Testing
1. On each endpoint PC (`Admin-PC1`, `Finance-PC1`, `IT-PC1`), switch IP configuration from Static to DHCP.
2. Confirm that each host obtains:
   * Correct subnet IP within designated lease range.
   * Correct subnet mask.
   * Correct default gateway.
   * Correct DNS server.

## 4. Expected Outcomes & Verification
1. `show ip dhcp binding` on `Northstar-R1` lists dynamic bindings with client MAC addresses.
2. `show ip dhcp pool` shows pool utilization and lease counts.
3. Endpoints maintain full internal and cross-VLAN network communication using dynamic leases.

## 5. Required Evidence Artifacts
* Router output: `show ip dhcp binding`.
* Endpoint screenshots/logs: `ipconfig /all` displaying dynamic lease parameters.
