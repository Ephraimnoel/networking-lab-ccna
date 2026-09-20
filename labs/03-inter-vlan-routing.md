# Lab 03 — Inter-VLAN Routing (Router-on-a-Stick)

**Status: Planned / Simulation Ready**  
*Simulator: Cisco Packet Tracer*

---

## 1. Objective
Configure Router-on-a-Stick (ROAS) on `Northstar-R1` using 802.1Q subinterfaces, assign default gateways for all departmental VLANs and the management segment, and verify routed cross-VLAN communication.

## 2. Prerequisites
* Lab 02 completed and verified.
* Addressing plan reviewed ([`docs/ip-addressing-plan.md`](../docs/ip-addressing-plan.md)).

## 3. Guided Implementation Tasks

### Task 3.1: Physical Uplink Enablement
On `Northstar-R1`:
```cisco
enable
configure terminal
hostname Northstar-R1
interface GigabitEthernet0/0
 description TRUNK_UPLINK_TO_SW1
 no ip address
 no shutdown
exit
```

### Task 3.2: Subinterface Configuration & 802.1Q Encapsulation
```cisco
! Administration Gateway
interface GigabitEthernet0/0.10
 description DEFAULT_GATEWAY_VLAN10_ADMIN
 encapsulation dot1Q 10
 ip address 10.10.10.1 255.255.255.224
exit

! Finance Gateway
interface GigabitEthernet0/0.20
 description DEFAULT_GATEWAY_VLAN20_FINANCE
 encapsulation dot1Q 20
 ip address 10.10.20.1 255.255.255.240
exit

! IT Gateway
interface GigabitEthernet0/0.30
 description DEFAULT_GATEWAY_VLAN30_IT
 encapsulation dot1Q 30
 ip address 10.10.30.1 255.255.255.224
exit

! Management Native Gateway
interface GigabitEthernet0/0.99
 description DEFAULT_GATEWAY_VLAN99_MGMT
 encapsulation dot1Q 99 native
 ip address 10.10.99.1 255.255.255.240
exit
```

## 4. Expected Outcomes & Verification
1. `show ip interface brief` on `Northstar-R1` confirms all subinterfaces are `Status: Up`, `Protocol: Up`.
2. `show ip route` shows directly connected routes for `10.10.10.0/27`, `10.10.20.0/28`, `10.10.30.0/27`, and `10.10.99.0/28`.
3. Ping from `Admin-PC1` to default gateway `10.10.10.1` succeeds.
4. Ping from `Admin-PC1` to `Finance-PC1` (`10.10.20.10`) succeeds via Layer 3 routing.

## 5. Required Evidence Artifacts
* Command text log: `show ip route` on router.
* Command text log: `show ip interface brief` on router.
* ICMP test log: Successful cross-VLAN ping and traceroute demonstrating hop through `10.10.10.1`.
