# Project Progression Checklist

**Project:** Northstar Services CCNA Network Lab  
**Current Overall Status:** **In Progress (Design, Specifications, & IOS Config Scripts Completed; Lab Simulation Execution Pending)**

---

## 1. Network Design & Requirements
- [x] **Completed** — Define business scenario and user sizing requirements ([`docs/network-requirements.md`](docs/network-requirements.md))
- [x] **Completed** — Define functional and non-functional engineering requirements
- [x] **Completed** — Design logical network architecture and visual Mermaid topology ([`diagrams/network-topology.md`](diagrams/network-topology.md))
- [x] **Completed** — Map device roles and switchport allocations

## 2. IP Addressing & VLSM Subnetting
- [x] **Completed** — Allocate RFC 1918 private address space (`10.10.0.0/16`)
- [x] **Completed** — Calculate VLSM subnets matching departmental sizes ([`docs/ip-addressing-plan.md`](docs/ip-addressing-plan.md))
- [x] **Completed** — Define static infrastructure reservations and default gateways
- [x] **Completed** — Design DHCP pools and exclusion ranges

## 3. VLAN Segmentation & Layer 2 Switching
- [x] **Completed** — Specify VLAN IDs, names, and security categories ([`docs/vlan-plan.md`](docs/vlan-plan.md))
- [x] **Completed** — Design 802.1Q trunk link and select dedicated Native VLAN 99
- [x] **Completed** — Define port allocation and unused port parking policy
- [ ] **Planned** — Execute Lab 01: Build basic switching topology in Packet Tracer ([`labs/01-basic-switching.md`](labs/01-basic-switching.md))
- [ ] **Planned** — Execute Lab 02: Configure VLANs and trunks in Packet Tracer ([`labs/02-vlans-and-trunks.md`](labs/02-vlans-and-trunks.md))

## 4. Inter-VLAN Routing & DHCP Services
- [x] **Completed** — Design Router-on-a-Stick subinterface architecture
- [x] **Completed** — Design centralized Cisco IOS DHCP pools
- [ ] **Planned** — Execute Lab 03: Configure subinterfaces on `Northstar-R1` in Packet Tracer ([`labs/03-inter-vlan-routing.md`](labs/03-inter-vlan-routing.md))
- [ ] **Planned** — Execute Lab 04: Configure DHCP exclusions, pools, and verify client leases ([`labs/04-dhcp.md`](labs/04-dhcp.md))

## 5. Network Security & Device Hardening
- [x] **Completed** — Author foundational switch and router security baseline ([`docs/security-baseline.md`](docs/security-baseline.md))
- [x] **Completed** — Define port security controls (sticky MAC, violation modes)
- [x] **Completed** — Specify SSHv2 and management line protections
- [ ] **Planned** — Execute Lab 06: Apply security baseline and test port security in Packet Tracer ([`labs/06-security-baseline.md`](labs/06-security-baseline.md))

## 6. Systematic Troubleshooting & Fault Injection
- [x] **Completed** — Document 8-stage hypothesis-driven troubleshooting framework ([`docs/troubleshooting-log.md`](docs/troubleshooting-log.md))
- [x] **Completed** — Formulate 3 controlled fault test scenarios
- [ ] **Planned** — Execute Lab 05: Inject and troubleshoot Fault 01 (VLAN access mismatch)
- [ ] **Planned** — Execute Lab 05: Inject and troubleshoot Fault 02 (Trunk allowed-list omission)
- [ ] **Planned** — Execute Lab 05: Inject and troubleshoot Fault 03 (Subinterface encapsulation mismatch)

## 7. Configuration Scripts & Evidence Framework
- [x] **Completed** — Author ready-to-deploy Cisco IOS router and switch configuration scripts ([`configs/`](configs/))
- [x] **Completed** — Establish evidence directory layout and naming standards ([`evidence/README.md`](evidence/README.md))
- [ ] **Planned** — Save baseline `.pkt` file and export topology screenshot
- [ ] **Planned** — Capture verified command outputs (`show vlan`, `show interfaces trunk`, `show ip route`)
- [ ] **Planned** — Capture ping and traceroute connectivity logs
- [ ] **Planned** — Capture post-troubleshooting sanitized device outputs

## 8. Final Report & Documentation
- [x] **Completed** — Establish final report structure ([`docs/final-report.md`](docs/final-report.md))
- [ ] **Planned** — Record actual test results, observations, and Packet Tracer metrics
- [ ] **Planned** — Review documentation for technical accuracy and complete project delivery
