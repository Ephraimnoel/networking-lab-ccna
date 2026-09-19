# IP Addressing Plan

**Status: Proposed / Planned — not implemented**

This plan is a starting point for the Packet Tracer lab. I must validate it against the final topology and update it if implementation requires changes.

## Proposed internal ranges

| VLAN | Department | Network | Prefix | Proposed gateway | Usable host range |
|---:|---|---|---|---|---|
| 10 | Administration | 10.10.10.0 | /27 | 10.10.10.1 | 10.10.10.1–10.10.10.30 |
| 20 | Finance | 10.10.20.0 | /28 | 10.10.20.1 | 10.10.20.1–10.10.20.14 |
| 30 | IT | 10.10.30.0 | /27 | 10.10.30.1 | 10.10.30.1–10.10.30.30 |
| 99 | Management/native (optional) | 10.10.99.0 | /28 | 10.10.99.1 | 10.10.99.1–10.10.99.14 |

## Proposed infrastructure reservations

| Purpose | Proposed address | Actual result |
|---|---|---|
| Administration gateway | 10.10.10.1 | To be implemented and verified |
| Finance gateway | 10.10.20.1 | To be implemented and verified |
| IT gateway | 10.10.30.1 | To be implemented and verified |
| Management gateway | 10.10.99.1 | To be decided |
| DHCP exclusions | To be decided | To be documented after implementation |

## Addressing decisions to make

- Confirm whether VLAN 99 is needed in the final Packet Tracer design.
- Decide how many end devices to model per department.
- Decide which addresses are reserved for infrastructure.
- Record any changes in the final report.

No address in this document is evidence that an interface, host, or DHCP scope has been configured.
