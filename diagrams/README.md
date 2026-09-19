# Diagrams

**Status: Planned architecture — not an implementation record**

Create the final diagram after building the topology. The diagram below describes the intended structure only:

```text
Internet / simulated edge
          |
        Router
          |
  Core / distribution switch
      /        |        \
 Admin VLAN  Finance VLAN  IT VLAN
```

## Final diagram requirements

The completed diagram should show:

- Internet or simulated edge, clearly labeled as simulated if applicable
- Router and switch roles
- Trunk links
- VLAN IDs and names
- Department segments
- Representative endpoints
- Subnets or gateway addresses where helpful
- A legend and a note that the design is a Packet Tracer lab

## Suggested files

- `network-topology.drawio` — editable source
- `network-topology.png` — exported image for the README
- `final-architecture-notes.md` — explanation of design choices

Do not label the planned diagram as a completed network. Update the status only after the topology has actually been built and the diagram matches the tested implementation.
