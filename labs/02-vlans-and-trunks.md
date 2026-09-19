# Lab 02 — VLANs and Trunks

**Status: Planned**

## Objective

Create department VLANs, assign access ports, and configure a trunk for links that carry multiple VLANs.

## Scenario

Administration, Finance, and IT endpoints must be logically separated even when they share switching infrastructure.

## Prerequisites

- Lab 01 topology built and understood
- VLAN plan reviewed
- Port roles identified

## Tasks to perform

1. Create VLANs 10, 20, and 30; decide whether VLAN 99 is required.
2. Name VLANs according to the VLAN plan.
3. Assign selected endpoint ports as access ports.
4. Configure the inter-switch or switch-router link as a trunk where required.
5. Verify VLAN membership and trunk status.
6. Test expected same-VLAN and blocked cross-VLAN behavior before routing is added.

## Commands/concepts to investigate

- `show vlan brief`
- `show interfaces trunk`
- `switchport mode access`
- `switchport access vlan`
- `switchport mode trunk`
- 802.1Q tags, native VLAN, access versus trunk mode

## Expected outcome

Department ports should be associated with the intended VLANs, and the required trunk should carry the intended VLANs. Actual success must be verified and documented.

## Evidence to capture

- VLAN table output
- Trunk output
- Port assignment table
- Screenshot of the topology
- Connectivity tests performed before routing

## Completion criteria

- VLANs and port assignments were configured personally.
- Trunk behavior was verified.
- Any unexpected behavior was documented rather than hidden.
