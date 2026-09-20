# Lab 02 — VLAN Segmentation & 802.1Q Trunks

**Status: Planned / Simulation Ready**  
*Simulator: Cisco Packet Tracer*

---

## 1. Objective
Create departmental VLANs (10, 20, 30, 99, 999), assign access ports, configure an 802.1Q trunk link to the router uplink, reassign the native VLAN, and verify that cross-VLAN traffic is blocked at Layer 2.

## 2. Prerequisites
* Lab 01 completed.
* VLAN Plan reviewed ([`docs/vlan-plan.md`](../docs/vlan-plan.md)).

## 3. Guided Implementation Tasks

### Task 3.1: VLAN Database Creation
On `Northstar-SW1`:
```cisco
enable
configure terminal
vlan 10
 name ADMIN
vlan 20
 name FINANCE
vlan 30
 name IT
vlan 99
 name MGMT_NATIVE
vlan 999
 name BLACKHOLE
exit
```

### Task 3.2: Access Port Assignment & DTP Disabling
```cisco
interface range FastEthernet0/2 - 5
 description ACCESS_ADMIN_VLAN10
 switchport mode access
 switchport access vlan 10
 switchport nonegotiate
exit

interface range FastEthernet0/6 - 10
 description ACCESS_FINANCE_VLAN20
 switchport mode access
 switchport access vlan 20
 switchport nonegotiate
exit

interface range FastEthernet0/11 - 15
 description ACCESS_IT_VLAN30
 switchport mode access
 switchport access vlan 30
 switchport nonegotiate
exit
```

### Task 3.3: 802.1Q Trunk Configuration & Native VLAN Reassignment
```cisco
interface FastEthernet0/1
 description UPLINK_TO_ROUTER_R1
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,30,99
 switchport nonegotiate
exit
```

### Task 3.4: Switch Virtual Interface (SVI) Management IP
```cisco
interface Vlan99
 description MANAGEMENT_SVI
 ip address 10.10.99.2 255.255.255.240
 no shutdown
exit
ip default-gateway 10.10.99.1
```

## 4. Expected Outcomes & Verification
1. `show vlan brief` confirms correct naming and port memberships.
2. `show interfaces trunk` confirms `Fa0/1` is in trunk mode with Native VLAN 99 and allowed VLANs `10, 20, 30, 99`.
3. **Cross-VLAN Isolation Test:** A ping from `Admin-PC1` (`10.10.10.10` in VLAN 10) to `Finance-PC1` (`10.10.20.10` in VLAN 20) **must fail** because routing has not yet been introduced.

## 5. Required Evidence Artifacts
* Command text output: `show vlan brief`.
* Command text output: `show interfaces trunk`.
* Command text output: Negative ping test showing cross-VLAN broadcast containment.
