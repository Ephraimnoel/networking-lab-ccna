# Device Configuration Scripts & Templates

**Status: Ready-to-Deploy Configuration Scripts (Cisco IOS)**  
*Target Hardware / Simulator: Cisco Packet Tracer 8.x*

This directory provides clean, modular, and fully commented Cisco IOS configuration scripts for the Northstar Services network lab. These scripts can be reviewed and pasted directly into the Cisco IOS Command Line Interface (CLI) of the respective devices in Cisco Packet Tracer.

---

## Included Configuration Scripts

| File | Device Target | Role & Key Features |
|---|---|---|
| [`R1-router-config.txt`](R1-router-config.txt) | Cisco 2911 / 1941 Router (`Northstar-R1`) | Router-on-a-Stick (ROAS) subinterfaces, 802.1Q encapsulation, DHCP pools, exclusion ranges, simulated WAN gateway |
| [`SW1-switch-config.txt`](SW1-switch-config.txt) | Cisco Catalyst 2960-24TT Switch (`Northstar-SW1`) | VLAN database, 802.1Q trunking, Native VLAN 99, access ports, unused port blackholing, port security, SSHv2, management SVI |

---

## Packet Tracer Quick Deployment Instructions

### Setting Up Northstar-R1 (Edge Router)
1. Add a **Cisco 2911** router to your Packet Tracer workspace.
2. Click the router, select the **CLI** tab.
3. When prompted: `Would you like to enter the initial configuration dialog? [yes/no]:`, type `no` and press Enter.
4. Enter privileged EXEC mode: `enable`
5. Enter global configuration: `configure terminal`
6. Copy the contents of [`R1-router-config.txt`](R1-router-config.txt) and paste directly into the CLI.
7. Save the running configuration: `copy running-config startup-config` (or `write memory`).

### Setting Up Northstar-SW1 (Core Access Switch)
1. Add a **Cisco Catalyst 2960-24TT** switch to your Packet Tracer workspace.
2. Click the switch, select the **CLI** tab, press Enter.
3. Enter privileged EXEC mode: `enable`
4. Enter global configuration: `configure terminal`
5. Copy the contents of [`SW1-switch-config.txt`](SW1-switch-config.txt) and paste directly into the CLI.
6. Save the running configuration: `copy running-config startup-config`.

### Connecting Cables
* Connect a **Copper Straight-Through** cable between:
  * Router `GigabitEthernet 0/0` <---> Switch `FastEthernet 0/1` (Trunk Uplink)
* Connect endpoint PCs to switchports according to departmental allocations:
  * `Admin-PC1` & `Admin-PC2`: Switchports `Fa0/2` and `Fa0/3` (VLAN 10)
  * `Finance-PC1` & `Finance-PC2`: Switchports `Fa0/6` and `Fa0/7` (VLAN 20)
  * `IT-PC1`: Switchport `Fa0/11` (VLAN 30)
* Set each PC to **DHCP** in its desktop IP configuration window to verify lease acquisition.
