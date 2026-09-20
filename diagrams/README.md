# Network Topology & Visual Assets

**Status: Planned Architecture / Design Documentation**

This directory houses the logical architecture, diagram source files, and visual exports for the CCNA Networking Lab project.

---

## Architecture Diagram

The logical network architecture is documented in detail in [`network-topology.md`](network-topology.md).

```mermaid
graph LR
    WAN["Simulated WAN<br/>192.0.2.1/30"] --- R1["Router: Northstar-R1<br/>(ROAS Gateway)"]
    R1 ===|802.1Q Trunk| SW1["Switch: Northstar-SW1<br/>(Catalyst 2960)"]
    SW1 --- V10["VLAN 10: Admin<br/>10.10.10.0/27"]
    SW1 --- V20["VLAN 20: Finance<br/>10.10.20.0/28"]
    SW1 --- V30["VLAN 30: IT<br/>10.10.30.0/27"]
    SW1 -.- V99["VLAN 99: Mgmt SVI<br/>10.10.99.0/28"]
```

---

## Included Files & Asset Guidelines

* [`network-topology.md`](network-topology.md) — Comprehensive technical breakdown of the Layer 2/3 topology, interface assignments, and broadcast domains.
* `network-topology.drawio` *(Planned)* — Editable XML source file created in diagrams.net / draw.io.
* `network-topology.png` *(Planned)* — High-resolution exported image for external documentation and PDF reports.

> **Authenticity Note:** The diagram above reflects the planned engineering design. When Packet Tracer topology files (`.pkt`) and screenshots are produced during lab execution, corresponding screenshots will be added to `evidence/screenshots/`.
