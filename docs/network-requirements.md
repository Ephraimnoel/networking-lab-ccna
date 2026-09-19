# Network Requirements

**Status: Planned**

## Scenario

Northstar Services is a fictional small business with approximately 30–50 users in Administration, Finance, and IT. The lab will model a logically segmented IPv4 network in Cisco Packet Tracer.

## Functional requirements

1. Provide a separate VLAN for each department.
2. Provide a documented IP subnet and default gateway for each VLAN.
3. Connect end devices through access ports.
4. Use a trunk where multiple VLANs traverse a shared link.
5. Provide inter-VLAN routing after the switching baseline is verified.
6. Provide DHCP after routing and VLAN behavior are understood.
7. Verify expected connectivity with recorded tests.
8. Introduce and troubleshoot three controlled faults.

## Non-functional requirements

- Use RFC1918 private IPv4 addressing for internal networks.
- Keep the design understandable and resource-conscious.
- Document assumptions and changes.
- Do not publish credentials or sensitive information.
- Distinguish planned design from tested behavior.

## Scope boundaries

This is a learning simulation. It does not model every production requirement, including high availability, wireless design, enterprise identity, real Internet access, or production change control.

## Acceptance criteria

The project may be marked complete only when the topology is built, each planned lab has been performed, baseline and fault-testing evidence is captured, documentation is updated with actual results, and the final report is reviewed.
