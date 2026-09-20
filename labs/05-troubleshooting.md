# Lab 05 — Controlled Fault Troubleshooting Exercises

**Status: Planned / Simulation Ready**  
*Simulator: Cisco Packet Tracer*

---

## 1. Objective
Practice hypothesis-driven troubleshooting by deliberately introducing, diagnosing, isolating, and rectifying three controlled network faults across Layer 2 switching, trunking, and Layer 3 routing.

## 2. Prerequisites
* Labs 01 through 04 completed with working baseline saved as `Northstar-Baseline.pkt`.
* Review Troubleshooting Framework in [`docs/troubleshooting-log.md`](../docs/troubleshooting-log.md).

## 3. Controlled Exercises

### Exercise 5.1: Diagnosing Access Port VLAN Misconfiguration
* **Injected Fault:** Switchport `Fa0/2` reassigned to VLAN 20.
* **Testing Protocol:**
  1. Record symptoms from `Admin-PC1`.
  2. Follow OSI Layer 2 diagnosis (`show mac address-table`, `show vlan brief`).
  3. Correct configuration.
  4. Verify resolution and log in [`docs/troubleshooting-log.md`](../docs/troubleshooting-log.md).

### Exercise 5.2: Diagnosing Trunk Pruning Omission
* **Injected Fault:** Trunk allowed VLAN list restricted to omit VLAN 30.
* **Testing Protocol:**
  1. Record symptom of IT host inability to reach default gateway.
  2. Inspect trunk status on switch (`show interfaces trunk`).
  3. Restore VLAN 30 to allowed list.
  4. Verify ping restoration and log findings.

### Exercise 5.3: Diagnosing Subinterface Encapsulation Mismatch
* **Injected Fault:** Router subinterface `g0/0.20` encapsulation altered to `dot1Q 25`.
* **Testing Protocol:**
  1. Observe that same-VLAN switching works, but gateway ping fails.
  2. Inspect router running-configuration for subinterface `g0/0.20`.
  3. Correct encapsulation tag to match VLAN 20.
  4. Verify inter-VLAN routing restoration.

## 4. Required Evidence Artifacts
* Pre-fix and post-fix command outputs for each fault.
* Completed investigation log entries in [`docs/troubleshooting-log.md`](../docs/troubleshooting-log.md).
