# CCNA Network Engineering Labs

**Abdulaziz | Hands-on networking portfolio | Cisco Packet Tracer**

I am building practical networking skills through Jeremy's IT Lab and documenting each completed exercise here. Each lab connects the task to the evidence: what I built, the skills practiced, and what the results actually demonstrate.

## Start Here

[Explore Lab 01: Packet Tracer Introduction](Labs/Lab-01-Packet-Tracer-Introduction.md) — a two-branch topology with 12 devices, labeled endpoints, and documented connections.

**Current progress:** six lab writeups with screenshot evidence: topology construction, connecting devices, OSI/DHCP analysis, basic device security, Ethernet switching, and IPv4 router configuration. Saved Packet Tracer files are pending. Verification results are recorded separately for each lab.

## Lab Progress

| Lab | Topic | Skills demonstrated | Status | Evidence |
| --- | --- | --- | --- | --- |
| 01 | [Packet Tracer Introduction](Labs/Lab-01-Packet-Tracer-Introduction.md) | Device placement, labeling, topology construction, automatic cable selection | Topology complete | [Topology screenshot](Photos/Day-01/01-completed-network-topology.png); `.pkt` pending |
| 02 | [Connecting Devices](Labs/Lab-02-Connecting-Devices.md) | Cable selection, device connections, distance considerations | Cabling documented | [Topology screenshot](Photos/Day-02/01-completed-network-topology.png); `.pkt` pending |
| 03 | [OSI Model & DHCP Packet Analysis](Labs/Lab-03-OSI-Model-DHCP-Packet-Analysis.md) | Simulation mode, OSPF PDU analysis, DHCP release/renew | Exercise complete; renewal result pending | [Simulation screenshot](Photos/Day-03/01-simulation-mode-traffic-analysis.png); `.pkt` pending |
| 04 | [Basic Device Security](Labs/Lab-04-Basic-Device-Security.md) | CLI modes, enable credentials, configuration saves | R1 verified; SW1 evidence pending | [R1 screenshot](Photos/Day-04/01-r1-password-configuration.png) and CLI excerpts; `.pkt` pending |
| 06 | [Ethernet LAN Switching](Labs/Lab-06-Ethernet-LAN-Switching-1.md) | ARP/ICMP analysis, MAC learning, table clearing | Ping and table checks verified | [Screenshots](Photos/Day-06/); `.pkt` pending |
| 08 | [IPv4 Address Configuration](Labs/Lab-08-IPv4-Address-Configuration.md) | Router interfaces, default gateways, cross-subnet ping tests | Interfaces and documented pings verified | [Screenshots](Photos/Lab-08/); `.pkt` pending |

## Skills Demonstrated So Far

- Navigate Packet Tracer's logical workspace and device catalog.
- Place and identify routers, switches, firewalls, PCs, servers, and a laptop.
- Arrange and label a two-branch network topology.
- Connect devices using automatic connection selection.
- Analyze simulated traffic and relate DHCP encapsulation to the OSI model.
- Configure privileged access and verify saved IOS settings.
- Configure IPv4 router interfaces and host gateways, then verify communication across subnets.
- Document visible results and distinguish a constructed topology from verified connectivity.

## Planned Learning

Upcoming work will cover Cisco IOS, Ethernet switching, IPv4 addressing and subnetting, routing, VLANs, STP, EtherChannel, OSPF, IPv6, ACLs, DHCP, NAT/PAT, security, and troubleshooting. These are planned topics; completed work appears in the lab progress table as evidence becomes available.

## Repository Structure

```text
ccna-network-engineering-labs/
├── README.md
├── Photos/
│   ├── Day-01/
│   │   └── 01-completed-network-topology.png
│   ├── Day-02/
│   │   └── 01-completed-network-topology.png
│   ├── Day-03/
│   │   ├── 01-simulation-mode-traffic-analysis.png
│   │   ├── 02-pc1-dhcp-release-renew.png
│   │   └── 03-ospf-hello-osi-layers.png
│   ├── Day-04/
│   │   ├── 01-r1-password-configuration.png
│   │   └── reference-examples/
│   ├── Day-06/  (six screenshots)
│   └── Lab-08/  (eleven screenshots)
└── Labs/
    ├── Lab-01-Packet-Tracer-Introduction.md
    ├── Lab-02-Connecting-Devices.md
    ├── Lab-03-OSI-Model-DHCP-Packet-Analysis.md
    ├── Lab-04-Basic-Device-Security.md
    ├── Lab-06-Ethernet-LAN-Switching-1.md
    └── Lab-08-IPv4-Address-Configuration.md
```

**[Labs](Labs/)** contains the writeups, named by lab number and topic. **[Photos](Photos/)** contains the original lab screenshots, grouped by lab.

New writeups appear directly under `Labs` by lab number and topic. Labs 05 and 07 have not been documented; numbering follows the course rather than implying every preceding lab is complete. The saved Lab 01 Packet Tracer file will be added to `Labs` when supplied.

## Documentation Approach

Each lab presents an overview, topology image, objectives, device inventory, completed tasks, verification, and lessons learned. Configuration labs will also include addressing tables, relevant commands, and troubleshooting results.

## Learning Resources and Credits

- **Course:** Jeremy's IT Lab, Day 1 — Packet Tracer Introduction.
- **Portfolio organization inspiration:** [TushanDorsey's Network Engineering Labs](https://github.com/TushanDorsey/Network-Engineering-Labs-CCNA-2026). All lab writeups describe my own completed work.
- **GitHub:** [Abdulaziz998](https://github.com/Abdulaziz998)
