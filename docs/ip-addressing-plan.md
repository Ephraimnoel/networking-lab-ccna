# IP Addressing & Subnetting Plan

**Status: Proposed / Design Baseline (RFC 1918 & RFC 5737 Compliant)**  
*Organization: Northstar Services (Fictional Small Business Scenario)*

---

## 1. Design Overview

The addressing plan uses the RFC 1918 private block `10.10.0.0/16` and applies **Variable Length Subnet Masking (VLSM)** to right-size departmental subnets based on projected endpoint counts. This ensures efficient address allocation, limits broadcast domain scope, and provides headroom for future device growth.

### Departmental Sizing Requirements
* **Administration:** 15–20 endpoints (workstations, shared printers, reception).
* **Finance:** 8–12 endpoints (accounting PCs, payroll devices, secure workstations).
* **IT & Infrastructure:** 7–18 endpoints (IT support workstations, testing stations, local servers).
* **Network Management:** 2–6 devices (switch SVIs, router management interfaces, future out-of-band tools).

---

## 2. Subnet Allocation Matrix

| VLAN | Department / Role | Network Address | Prefix | Subnet Mask | Usable Host Range | Default Gateway | Broadcast Address | Total Usable Hosts | Planned Capacity |
|:---:|---|---|:---:|---|---|---|---|:---:|:---:|
| **10** | Administration | `10.10.10.0` | `/27` | `255.255.255.224` | `10.10.10.1` – `10.10.10.30` | `10.10.10.1` | `10.10.10.31` | 30 | 15–20 hosts |
| **20** | Finance | `10.10.20.0` | `/28` | `255.255.255.240` | `10.10.20.1` – `10.10.20.14` | `10.10.20.1` | `10.10.20.15` | 14 | 8–12 hosts |
| **30** | IT & Infrastructure | `10.10.30.0` | `/27` | `255.255.255.224` | `10.10.30.1` – `10.10.30.30` | `10.10.30.1` | `10.10.30.31` | 30 | 7–18 hosts |
| **99** | Management / Native | `10.10.99.0` | `/28` | `255.255.255.240` | `10.10.99.1` – `10.10.99.14` | `10.10.99.1` | `10.10.99.15` | 14 | 2–6 devices |
| **—** | Simulated Edge / WAN | `192.0.2.0` | `/30` | `255.255.255.252` | `192.0.2.1` – `192.0.2.2` | `192.0.2.1` (ISP) | `192.0.2.3` | 2 | Point-to-point link |

*Note: The `192.0.2.0/30` network is drawn from RFC 5737 (TEST-NET-1) reserved for documentation and simulation examples.*

---

## 3. Infrastructure Reservations & DHCP Allocation

Dynamic Host Configuration Protocol (DHCP) will be hosted on `Northstar-R1`. Low-order IP addresses in each client subnet are excluded from the dynamic pools to accommodate static infrastructure, default gateways, and network printers.

| VLAN | Subnet | Excluded Range (Static Reservations) | DHCP Pool Name | Dynamic Lease Range | Dynamic Leases Available |
|:---:|---|---|---|---|:---:|
| **10** | `10.10.10.0/27` | `10.10.10.1` – `10.10.10.9` | `ADMIN_POOL` | `10.10.10.10` – `10.10.10.30` | 21 |
| **20** | `10.10.20.0/28` | `10.10.20.1` – `10.10.20.4` | `FINANCE_POOL` | `10.10.20.5` – `10.10.20.14` | 10 |
| **30** | `10.10.30.0/27` | `10.10.30.1` – `10.10.30.9` | `IT_POOL` | `10.10.30.10` – `10.10.30.30` | 21 |
| **99** | `10.10.99.0/28` | All addresses (`10.10.99.1` – `10.10.99.14`) | *(None — Static Only)* | N/A | 0 |

### Specific Static Device Assignments
* **`Northstar-R1` (Default Gateways):**
  * `g0/0.10`: `10.10.10.1/27`
  * `g0/0.20`: `10.10.20.1/28`
  * `g0/0.30`: `10.10.30.1/27`
  * `g0/0.99`: `10.10.99.1/28`
  * `g0/1`: `192.0.2.2/30`
* **`Northstar-SW1` (Switch Virtual Interface):**
  * `interface Vlan99`: `10.10.99.2/28`
  * Default gateway: `10.10.99.1`
* **Local Test Server (VLAN 30):**
  * Static IP: `10.10.30.5/27` (Gateway: `10.10.30.1`)

---

## 4. VLSM Mathematical Justification

1. **VLAN 10 (Admin):** Requirements state 15–20 users. A `/28` mask yields only 14 usable addresses (insufficient). A `/27` provides 30 usable host addresses ($2^{5} - 2 = 30$), accommodating current needs plus 50% growth margin.
2. **VLAN 20 (Finance):** Requirements state 8–12 users. A `/28` mask provides 14 usable addresses ($2^{4} - 2 = 14$), fitting the 12-user maximum with minimal address wastage.
3. **VLAN 30 (IT & Infrastructure):** Requirements state 7–18 endpoints. A `/28` is too restrictive for peak growth and static testing servers. A `/27` (30 hosts) ensures adequate testing space.
4. **VLAN 99 (Management):** Infrastructure management requires fewer than 5 active SVIs and interfaces. A `/28` provides 14 usable addresses, isolating administrative traffic from all user endpoints.
