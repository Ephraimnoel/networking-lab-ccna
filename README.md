# CCNA Networking Lab

[![Status: In Progress](https://img.shields.io/badge/status-in--progress-orange)](checklist.md)
[![Focus: Networking](https://img.shields.io/badge/focus-networking-blue)](README.md)

A hands-on Cisco Packet Tracer project for designing, configuring, verifying, and troubleshooting a small-business network. The lab is intentionally documented as an **In Progress** personal project: no configuration, test result, screenshot, or successful outcome is claimed until it is produced and recorded by me.

## Why I am building this

This project turns CCNA knowledge into practical evidence. It is designed to show that I can reason about network requirements, plan an addressing scheme, configure switching and routing, test connectivity, troubleshoot deliberately introduced faults, and communicate technical work clearly.

## Scenario

**Fictional organization:** Northstar Services, a small business with approximately 30–50 users.

The business has three departments:

| Department | Purpose | Planned users |
|---|---|---:|
| Administration | Operations, reception, and management | 15–20 |
| Finance | Financial and payroll operations | 8–12 |
| IT | Technical support and infrastructure administration | 7–18 |

Departments will be logically separated with VLANs. The design is a proposed lab scenario, not a real organization or production network.

## Planned architecture

```text
Internet / simulated edge
          |
      Router
          |
   Core / distribution switch
      /        |        \
 Admin VLAN  Finance VLAN  IT VLAN
```

See [`diagrams/README.md`](diagrams/README.md) for the diagram requirements. This architecture is **planned** and does not represent a completed implementation.

## Tools and technologies

- Cisco Packet Tracer
- Cisco IOS concepts and verification commands
- IPv4 subnetting and RFC1918 private addressing
- VLANs, access ports, and 802.1Q trunking
- Inter-VLAN routing
- DHCP
- Ping, traceroute, and structured troubleshooting
- Markdown, Git, and GitHub
- diagrams.net/draw.io for diagrams

## Networking concepts demonstrated

- Basic switching and MAC learning
- VLAN segmentation
- Access-port assignment
- Trunk links
- Router-on-a-stick or another approved inter-VLAN routing design
- Default gateways and DHCP
- Connectivity verification
- Basic device-management security
- Fault isolation and root-cause analysis
- Technical documentation

## Proposed addressing and VLAN design

The following is a proposed design and must be validated or changed during implementation. It is not evidence that the network has been configured.

| VLAN | Name | Proposed subnet | Proposed gateway | Planned capacity |
|---:|---|---|---|---:|
| 10 | Administration | 10.10.10.0/27 | 10.10.10.1 | 30 addresses |
| 20 | Finance | 10.10.20.0/28 | 10.10.20.1 | 14 addresses |
| 30 | IT | 10.10.30.0/27 | 10.10.30.1 | 30 addresses |
| 99 | Management/native (optional) | 10.10.99.0/28 | 10.10.99.1 | 14 addresses |
|
|  | Simulated edge/WAN | 192.0.2.0/30 | To be decided | Documentation-only example range |

The `192.0.2.0/30` range is reserved for documentation examples. It must not be treated as a real Internet connection.

Detailed planning documents are in [`docs/`](docs/).

## Current status

> 🚧 **Status: In Progress**
>
> The repository contains planning documents, lab instructions, templates, and checklists. The network has not yet been claimed as configured or tested. Completion status will change only after real implementation and evidence are added.

## Planned labs

| Lab | Topic | Status |
|---|---|---|
| 01 | Basic switching | Planned |
| 02 | VLANs and trunks | Planned |
| 03 | Inter-VLAN routing | Planned |
| 04 | DHCP | Planned |
| 05 | Troubleshooting deliberate faults | Planned |

The eventual workflow also includes basic device security, connectivity verification, evidence capture, and a final report.

## Evidence standard

For each completed activity, I will capture only evidence I personally generated, such as:

- The Packet Tracer `.pkt` file
- A topology screenshot
- VLAN and trunk verification output
- Routing-table and interface output
- DHCP allocation output
- Connectivity tests and their results
- Troubleshooting notes, including the failed state and corrected state
- Before/after screenshots where useful
- A final report that distinguishes planned design from tested behavior

I will remove or redact credentials, private information, tokens, and sensitive network details before publishing. See [`evidence/README.md`](evidence/README.md).

## What I personally need to complete

1. Install and open Cisco Packet Tracer.
2. Read the requirements and validate the proposed addressing plan.
3. Build the topology from the planned architecture.
4. Configure and verify each lab rather than copying an untested configuration.
5. Save the Packet Tracer file and capture evidence as I go.
6. Introduce the three controlled faults only after the baseline works.
7. Record symptoms, tests, root causes, corrections, and verification.
8. Complete the final report and review the checklist.

## Learning objectives

By the end of the lab, I should be able to:

- Translate a small-business scenario into a basic network design.
- Explain why VLANs and subnetting are useful.
- Configure and verify switching, trunks, routing, and DHCP in a simulator.
- Use evidence-based troubleshooting instead of guessing.
- Apply basic management-security considerations.
- Produce documentation that another beginner could follow.

## Disclaimer

This is a personal learning lab based on a fictional organization. It is not professional network administration experience, production change history, or evidence of employment. Any future results will be labeled according to what was actually performed and tested.

## Repository map

- [`checklist.md`](checklist.md) — project progress tracker
- [`docs/`](docs/) — requirements, plans, troubleshooting, and report templates
- [`labs/`](labs/) — guided exercises
- [`configs/README.md`](configs/README.md) — policy for adding personal configurations
- [`diagrams/README.md`](diagrams/README.md) — planned architecture diagram guidance
- [`evidence/README.md`](evidence/README.md) — evidence capture and safety guidance
