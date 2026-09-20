# Lab 01 — Basic Switching & MAC Learning

**Status: Planned / Simulation Ready**  
*Simulator: Cisco Packet Tracer*

---

## 1. Objective
Model the foundational Layer 2 switched network in Cisco Packet Tracer, verify physical link states, observe dynamic MAC address learning, and inspect frame forwarding before implementing VLAN segmentation.

## 2. Prerequisites
* Cisco Packet Tracer 8.x installed and operational.
* IP addressing plan reviewed ([`docs/ip-addressing-plan.md`](../docs/ip-addressing-plan.md)).
* Clean `.pkt` file initialized.

## 3. Topology & Device Inventory
* **Switch:** 1x Cisco Catalyst 2960-24TT (`Northstar-SW1`)
* **End Devices:** 
  * 2x Administration PCs (`Admin-PC1`, `Admin-PC2`)
  * 1x IT PC (`IT-PC1`)
* **Cabling:** Copper Straight-Through cables connecting PC NICs to switch FastEthernet ports.

## 4. Guided Implementation Tasks

### Task 4.1: Device Placement & Physical Connectivity
1. Place Cisco 2960 switch in the workspace and rename hostname to `Northstar-SW1`.
2. Connect `Admin-PC1` FastEthernet0 to switch `Fa0/2`.
3. Connect `Admin-PC2` FastEthernet0 to switch `Fa0/3`.
4. Connect `IT-PC1` FastEthernet0 to switch `Fa0/11`.
5. Observe STP transition from amber (listening/learning) to green (forwarding).

### Task 4.2: Initial Host Addressing (Flat Testing Baseline)
Configure static testing addresses to evaluate unsegmented communication:
* `Admin-PC1`: `10.10.10.10 / 255.255.255.0`
* `Admin-PC2`: `10.10.10.11 / 255.255.255.0`
* `IT-PC1`: `10.10.10.30 / 255.255.255.0`

### Task 4.3: Inspect Dynamic MAC Address Learning
1. On `Northstar-SW1`, inspect initial MAC table before traffic:
   ```cisco
   enable
   show mac address-table
   ```
2. From `Admin-PC1`, ping `Admin-PC2` (`10.10.10.11`).
3. Re-run `show mac address-table` on `Northstar-SW1` to observe learned dynamic MACs.

## 5. Expected Verification Outputs
* Link status verified via:
  ```cisco
  show interfaces status
  ```
* MAC address table shows active entries mapped to respective physical ports (`Fa0/2`, `Fa0/3`, `Fa0/11`) in default VLAN 1.

## 6. Required Evidence Artifacts
* Screenshot: Topology layout with green link lights.
* Command Log: `show mac address-table` captured post-ping.
* Output: ICMP ping reply between test endpoints.
