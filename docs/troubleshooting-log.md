# Systematic Troubleshooting Methodology & Fault Log

**Status: Standard Operating Procedure & Simulation Case Log**  
*Methodology: Hypothesis-Driven, OSI-Aligned Network Diagnostics*

---

## 1. Structured Troubleshooting Framework

To isolate network faults systematically rather than relying on trial-and-error guessing, this project enforces an 8-stage diagnostic workflow:

```text
1. Identify Symptom ──> 2. Gather Baseline Evidence ──> 3. Formulate Hypothesis
                                                                   │
8. Document & Close <── 7. Verify Resolution <── 6. Correct <── 5. Isolate Cause
```

### Stage Breakdown
1. **Identify the Symptom:** Define what is failing, who is affected (single host, entire VLAN, cross-VLAN), when it started, and what remains working.
2. **Gather Baseline Evidence:** Capture output without altering configuration (`ipconfig /all`, `ping`, `traceroute`, `show ip interface brief`, `show interfaces status`).
3. **Formulate Hypothesis (Bottom-Up OSI Model):**
   * *Layer 1 (Physical):* Cable connected, link lights green/amber, interface up/down?
   * *Layer 2 (Data Link):* Access port in right VLAN? Trunk tagging correct? Port-security violation shutdown?
   * *Layer 3 (Network):* IP address, subnet mask, default gateway correct? Route table entry present?
   * *Layer 4 / Services:* DHCP pool exhausted? ACL blocking traffic?
4. **Test the Hypothesis:** Run targeted non-destructive verification commands (`show vlan brief`, `show mac address-table`, `show ip route`).
5. **Isolate Root Cause:** Confirm the specific discrepancy between documented baseline design and actual device state.
6. **Implement Corrective Action:** Change exactly **one** variable at a time to isolate causality.
7. **Verify Full System Resolution:** Confirm that the failed service is restored AND verify that no unintended side effects were created.
8. **Document Findings & Lessons Learned:** Record symptoms, hypothesis, proof, fix, and prevention steps.

---

## 2. Planned Controlled Fault Scenarios (Simulation Studies)

These three fault scenarios will be deliberately introduced after the baseline network is verified in Cisco Packet Tracer:

---

### Fault Scenario 01: Endpoint Access Port VLAN Mismatch

* **Classification:** Layer 2 Configuration Error
* **Simulated Situation:** An administrator connects `Admin-PC1` to switchport `Fa0/6` (which belongs to Finance VLAN 20) instead of `Fa0/2` (VLAN 10).
* **Observed Symptom (Simulated):** `Admin-PC1` receives an IP lease in the `10.10.20.0/28` range instead of `10.10.10.0/27`, or fails to communicate with departmental printers in Admin VLAN 10.
* **Diagnostic Walkthrough:**
  1. *Host Check:* Run `ipconfig /all` on endpoint. Note assigned IP and gateway.
  2. *Switch Check:* Run `show mac address-table` on switch to identify which switchport learned the endpoint's MAC address.
  3. *VLAN Membership:* Run `show vlan brief` to check the VLAN assigned to that switchport.
  4. *Root Cause:* Port `Fa0/6` is assigned to `switchport access vlan 20`.
  5. *Correction:* Move endpoint to port `Fa0/2` or reconfigure port: `switchport access vlan 10`.
  6. *Verification:* Release and renew DHCP (`ipconfig /renew`); confirm IP in `10.10.10.0/27`; ping gateway `10.10.10.1`.

---

### Fault Scenario 02: Trunk Allowed-List Omission (Trunk Pruning Fault)

* **Classification:** Layer 2 Trunking / VLAN Encapsulation Error
* **Simulated Situation:** During manual trunk configuration on `Fa0/1`, the engineer executes `switchport trunk allowed vlan 10,20` and accidentally omits VLAN 30 and 99.
* **Observed Symptom (Simulated):** Administration and Finance hosts communicate normally with their gateways, but all IT endpoints (VLAN 30) and switch management access (VLAN 99) lose Layer 3 connectivity.
* **Diagnostic Walkthrough:**
  1. *Scope Check:* Admin ping to gateway succeeds; IT ping to gateway fails.
  2. *Switch Port Check:* Run `show interfaces trunk` on `Northstar-SW1`.
  3. *Observation:* "VLANs allowed on trunk" lists `10, 20`. VLANs 30 and 99 are absent.
  4. *Root Cause:* Incomplete allowed VLAN list on trunk link.
  5. *Correction:* `interface Fa0/1` -> `switchport trunk allowed vlan add 30,99`.
  6. *Verification:* `show interfaces trunk` confirms `10, 20, 30, 99`; IT host successfully pings gateway `10.10.30.1`.

---

### Fault Scenario 03: Subinterface Encapsulation ID Mismatch

* **Classification:** Layer 3 Inter-VLAN Routing Error
* **Simulated Situation:** On router `Northstar-R1`, subinterface `g0/0.20` is accidentally configured with `encapsulation dot1Q 25` instead of `20`.
* **Observed Symptom (Simulated):** Finance workstations (VLAN 20) can ping each other across the switch, but cannot ping their default gateway `10.10.20.1` or reach other subnets.
* **Diagnostic Walkthrough:**
  1. *Layer 2 Check:* `show vlan brief` confirms switchports are correctly in VLAN 20. Same-VLAN ping between Finance PCs succeeds.
  2. *Trunk Check:* `show interfaces trunk` confirms VLAN 20 is active and passing across trunk.
  3. *Router Check:* Run `show ip interface brief` and `show running-config interface g0/0.20`.
  4. *Root Cause:* 802.1Q encapsulation tag (`dot1Q 25`) does not match the incoming tagged frames from VLAN 20.
  5. *Correction:* Under `interface g0/0.20`, apply `encapsulation dot1Q 20`.
  6. *Verification:* Ping gateway `10.10.20.1` from `Finance-PC1`; test inter-VLAN ping to `Admin-PC1` (`10.10.10.x`).

---

## 3. Investigation Record Template (To be Completed During Testing)

```markdown
### Investigation Log #__ — [Title]
- **Date & Time:** [YYYY-MM-DD HH:MM]
- **Status:** [Planned / Under Investigation / Verified Resolved]
- **Affected Devices / Hosts:** [e.g., Finance-PC1, Northstar-SW1]
- **Observed Symptoms:** [Exact error message, ping loss percentage, IP output]
- **Initial Hypothesis:** [L1, L2, or L3 suspicion with rationale]
- **Commands Executed:**
  1. `command 1` — Result: [...]
  2. `command 2` — Result: [...]
- **Root Cause Identified:** [Specific technical explanation]
- **Remediation Steps Applied:** [Specific configuration commands entered]
- **Verification Retest:** [Post-remediation test results and evidence reference]
- **Preventative Action / Runbook Update:** [How to prevent recurrence]
```
