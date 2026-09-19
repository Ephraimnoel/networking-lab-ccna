# Lab 04 — DHCP

**Status: Planned**

## Objective

Provide dynamic IPv4 addressing to department endpoints and verify that leases match the planned network design.

## Scenario

A small IT team wants to reduce manual endpoint configuration while keeping gateway and address assignments documented.

## Prerequisites

- VLANs and inter-VLAN routing implemented and verified
- Addressing plan validated
- Infrastructure reservations identified

## Tasks to perform

1. Decide where DHCP will be provided in the simulated design.
2. Create one scope per required department network.
3. Exclude or reserve infrastructure addresses as appropriate.
4. Configure clients to obtain addresses dynamically.
5. Verify assigned addresses, masks, gateways, and DNS settings.
6. Test renewal or re-acquisition behavior where supported.

## Commands/concepts to investigate

- DHCP scope, pool, exclusion, lease, and relay concepts
- `show ip dhcp binding`
- `show ip dhcp pool`
- `show ip interface brief`
- Client IP configuration tools in Packet Tracer

## Expected outcome

Clients should receive addresses from the correct planned subnet after implementation. The actual lease results must be captured.

## Evidence to capture

- DHCP configuration evidence
- Binding/lease output
- Client IP configuration screenshots
- Connectivity tests using assigned addresses

## Completion criteria

- Each required scope was configured personally.
- At least one client per relevant VLAN was tested.
- Lease and gateway results were documented.
- No credentials or sensitive information were published.
