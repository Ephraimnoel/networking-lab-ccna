# VLAN Segmentation & Switchport Design Plan

**Status: Proposed / Design Baseline**  
*Switch: Cisco Catalyst 2960-24TT (`Northstar-SW1`)*

---

## 1. VLAN Segmentation Matrix

VLANs are configured to enforce Layer 2 separation between organizational units. Broadcast domains are isolated, preventing inter-departmental eavesdropping and broadcast storms from traversing boundaries without passing through the Layer 3 router.

| VLAN ID | VLAN Name | Subnet | Associated Department / Role | Security Classification | Access Policy |
|:---:|---|---|---|---|---|
| **10** | `ADMIN` | `10.10.10.0/27` | Administration, management, reception | General Business | Standard access; routes to IT and WAN |
| **20** | `FINANCE` | `10.10.20.0/28` | Financial records, accounting, payroll | Confidential / Sensitive | High restriction; candidate for ACL containment |
| **30** | `IT` | `10.10.30.0/27` | Systems support, technical workstations | Administrative | Privileged access; allowed management traversal |
| **99** | `MGMT_NATIVE` | `10.10.99.0/28` | Switch SVI, out-of-band network access | Critical Infrastructure | Isolated; no regular end-user hosts permitted |
| **999** | `BLACKHOLE` | *(Unassigned)* | Unused physical switchports | Security Quarantine | Administratively disabled (`shutdown`) |

---

## 2. Switchport Allocation & Interface Mapping

The 24 FastEthernet ports and 2 GigabitEthernet ports on `Northstar-SW1` are mapped systematically:

| Port Range | Port Mode | Assigned VLAN | Destination / Role | Hardening & Security Controls |
|---|---|---|---|---|
| `Fa0/1` | **Trunk (802.1Q)** | Allowed: `10,20,30,99` | Uplink to Router `Northstar-R1` (`g0/0`) | Native VLAN set to 99; DTP disabled (`nonegotiate`) |
| `Fa0/2 - Fa0/5` | **Access** | VLAN 10 (`ADMIN`) | Administration PC workstations & printer | Port security (max 2 MACs, sticky, restrict); DTP disabled |
| `Fa0/6 - Fa0/10` | **Access** | VLAN 20 (`FINANCE`) | Finance & payroll PC workstations | Port security (max 2 MACs, sticky, restrict); DTP disabled |
| `Fa0/11 - Fa0/15` | **Access** | VLAN 30 (`IT`) | IT support workstations & local services | Port security (max 2 MACs, sticky, restrict); DTP disabled |
| `Fa0/16 - Fa0/24` | **Access** | VLAN 999 (`BLACKHOLE`) | Unused access ports | Assigned to unused VLAN 999 and `shutdown` |
| `Gi0/1 - Gi0/2` | **Access** | VLAN 999 (`BLACKHOLE`) | Unused gigabit ports | Assigned to unused VLAN 999 and `shutdown` |

---

## 3. Trunking & Native VLAN Security Considerations

### Mitigation of Double-Tagging & VLAN Hopping Attacks
1. **Never Use VLAN 1 for User Traffic or Management:**
   Default Cisco IOS configurations assign all ports and native untagged traffic to VLAN 1. In this design, VLAN 1 is explicitly decommissioned for user data and management.
2. **Dedicated Native VLAN (VLAN 99):**
   The native VLAN on the 802.1Q trunk link (`Fa0/1`) is explicitly changed to VLAN 99 using:
   ```cisco
   switchport trunk native vlan 99
   switchport trunk allowed vlan 10,20,30,99
   ```
3. **Disable Dynamic Trunking Protocol (DTP):**
   Access ports should never attempt to negotiate trunking with connected endpoints. Every access port is statically defined and negotiation disabled:
   ```cisco
   switchport mode access
   switchport nonegotiate
   ```

---

## 4. Port Map Verification Template (Pre-Implementation)

This table will be updated with actual command verification outputs (`show vlan brief`, `show interfaces trunk`) during Lab 02 execution:

| Interface | Configured Mode | Operational Mode | Configured VLAN | Operational VLAN | Verification Command | Evidence Reference |
|---|---|---|---|---|---|---|
| `Fa0/1` | Trunk | Trunk | 10, 20, 30, 99 | 10, 20, 30, 99 | `show interfaces trunk` | Planned (Lab 02) |
| `Fa0/2` | Access | Access | 10 | 10 | `show vlan brief` | Planned (Lab 02) |
| `Fa0/6` | Access | Access | 20 | 20 | `show vlan brief` | Planned (Lab 02) |
| `Fa0/11`| Access | Access | 30 | 30 | `show vlan brief` | Planned (Lab 02) |
| `Fa0/16`| Access | Down | 999 | 999 | `show interfaces status` | Planned (Lab 02) |
