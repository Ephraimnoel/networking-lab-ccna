# Lab 03 — Inter-VLAN Routing

**Status: Planned**

## Objective

Provide Layer 3 routing between the planned department VLANs using a design you understand and can explain.

## Scenario

Departments need controlled communication through a router or Layer 3 switching design rather than direct Layer 2 adjacency.

## Prerequisites

- VLANs and trunking completed and verified
- Proposed gateways reviewed
- Routing design selected and documented

## Tasks to perform

1. Choose and document router-on-a-stick or another supported Packet Tracer design.
2. Configure the Layer 3 interfaces or subinterfaces.
3. Assign the planned gateway addresses.
4. Confirm interface status and routing information.
5. Test connectivity within and between VLANs.
6. Record whether the final policy allows all inter-VLAN traffic or requires restrictions.

## Commands/concepts to investigate

- `show ip interface brief`
- `show ip route`
- `show interfaces`
- `encapsulation dot1q`
- Default gateways and routing-table entries

## Expected outcome

Hosts should be able to reach permitted networks through the configured gateways after implementation. Do not claim this outcome before testing it.

## Evidence to capture

- Interface status
- Routing table
- Gateway configuration evidence
- Ping or other test results
- Updated architecture diagram

## Completion criteria

- Routing design is documented.
- Gateway interfaces were configured and verified.
- Inter-VLAN tests were personally performed.
- Actual results are added to the final report.
