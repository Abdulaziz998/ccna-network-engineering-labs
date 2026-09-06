# CCNA Network Engineering Labs

**Abdulaziz | Hands-on networking portfolio | Cisco Packet Tracer**

I am building practical networking skills through Jeremy's IT Lab and documenting each completed exercise here. Each lab connects the task to the evidence: what I built, the skills practiced, and what the results actually demonstrate.

## Start Here

[Explore Day 1: Packet Tracer Introduction](Labs/Day-01-Packet-Tracer-Introduction.md) — a two-branch topology with 12 devices, labeled endpoints, and documented connections.

**Current progress:** three lab writeups with screenshot evidence: topology construction, connecting devices, and OSI/DHCP traffic analysis. Saved Packet Tracer files and end-to-end connectivity verification are pending.

## Lab Progress

| Day | Lab | Skills demonstrated | Status | Evidence |
| --- | --- | --- | --- | --- |
| 01 | [Packet Tracer Introduction](Labs/Day-01-Packet-Tracer-Introduction.md) | Device placement, labeling, topology construction, automatic cable selection | Topology complete | [Topology screenshot](Photos/Day-01/01-completed-network-topology.png); `.pkt` pending |
| 02 | [Connecting Devices](Labs/Day-02-Connecting-Devices.md) | Cable selection, device connections, distance considerations | Cabling documented | [Topology screenshot](Photos/Day-02/01-completed-network-topology.png); `.pkt` pending |
| 03 | [OSI Model & DHCP Packet Analysis](Labs/Day-03-OSI-Model-DHCP-Packet-Analysis.md) | Simulation mode, OSPF PDU analysis, DHCP release/renew | Exercise complete; renewal result pending | [Simulation screenshot](Photos/Day-03/01-simulation-mode-traffic-analysis.png); `.pkt` pending |

## Skills Demonstrated So Far

- Navigate Packet Tracer's logical workspace and device catalog.
- Place and identify routers, switches, firewalls, PCs, servers, and a laptop.
- Arrange and label a two-branch network topology.
- Connect devices using automatic connection selection.
- Analyze simulated traffic and relate DHCP encapsulation to the OSI model.
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
│   └── Day-03/
│       ├── 01-simulation-mode-traffic-analysis.png
│       ├── 02-pc1-dhcp-release-renew.png
│       └── 03-ospf-hello-osi-layers.png
└── Labs/
    ├── Day-01-Packet-Tracer-Introduction.md
    ├── Day-02-Connecting-Devices.md
    └── Day-03-OSI-Model-DHCP-Packet-Analysis.md
```

**[Labs](Labs/)** contains the daily writeups, named by day and topic. **[Photos](Photos/)** contains the original lab screenshots, grouped by day.

Future writeups will appear directly under `Labs` as `Day-04-<Topic>.md`, `Day-05-<Topic>.md`, and so on as each lab is completed. The saved Day 1 Packet Tracer file will be added to `Labs` when supplied.

## Documentation Approach

Each lab presents an overview, topology image, objectives, device inventory, completed tasks, verification, and lessons learned. Configuration labs will also include addressing tables, relevant commands, and troubleshooting results.

## Learning Resources and Credits

- **Course:** Jeremy's IT Lab, Day 1 — Packet Tracer Introduction.
- **Portfolio organization inspiration:** [TushanDorsey's Network Engineering Labs](https://github.com/TushanDorsey/Network-Engineering-Labs-CCNA-2026). All lab writeups describe my own completed work.
- **GitHub:** [Abdulaziz998](https://github.com/Abdulaziz998)
