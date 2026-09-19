# VLAN Plan

**Status: Proposed / Planned — not implemented**

| VLAN ID | Name | Intended use | Planned access ports | Security/documentation notes |
|---:|---|---|---|---|
| 10 | ADMIN | Administration endpoints | To be assigned | Should not be used for Finance or IT endpoints |
| 20 | FINANCE | Finance endpoints | To be assigned | Treat as a sensitive business segment in the scenario |
| 30 | IT | IT endpoints and administration | To be assigned | Used for technical-management examples |
| 99 | MGMT/NATIVE | Optional management/native VLAN | To be decided | Use only if the final design requires it |

## Implementation notes

- Create VLANs deliberately and verify their names and IDs.
- Assign only the intended access ports.
- Configure trunks only on links that need to carry multiple VLANs.
- Document the final port map after implementation.
- Do not assume a VLAN is working because it exists; test it with an end device and verification commands.

## Final port map template

| Device | Interface | Mode | VLAN | Connected device/role | Evidence reference |
|---|---|---|---:|---|---|
| To be completed | To be completed | To be completed | To be completed | To be completed | To be completed |

## Questions to answer in the report

1. Why were these VLAN boundaries selected?
2. Which traffic should be allowed between VLANs in this lab?
3. What would change in a production design?
