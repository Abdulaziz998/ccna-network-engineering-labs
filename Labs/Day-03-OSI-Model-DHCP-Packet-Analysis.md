# Day 03 · Following Traffic Through the OSI Layers

[← Lab portfolio](../README.md)

**Focus:** Packet inspection and DHCP client behavior

**Environment:** Cisco Packet Tracer

## What I Investigated

With the network already connected, I moved into Simulation mode to examine what the devices were sending. I followed two parts of the exercise: inspecting background traffic and releasing PC1's address before requesting a lease again.

The saved captures document an OSPF Hello leaving R2 and the commands entered on PC1. Together, they show how packet information and client settings can be used to explain network behavior.

## The Network I Used

![Network layout and captured simulation events](../Photos/Day-03/01-simulation-mode-traffic-analysis.png)

PC1 reaches the local network through SW2, which connects to SW1. SRV1 and R1 also attach to SW1. A separate link joins R1 to R2.

| Part of the network | Details |
| --- | --- |
| Client | PC1, connected through SW2 |
| Switching | SW1 and SW2, Cisco 2960-24TT |
| Routing | R1 and R2, Cisco 2911 |
| Server | SRV1, labeled 192.168.1.100 |
| Local subnet | 192.168.1.0/24 |
| R1 LAN interface | G0/0, labeled 192.168.1.1 |
| Router link | 10.0.0.0/24; R1 G0/1 labeled .1, R2 G0/0 labeled .2 |

The topology provides the router and server labels. The captures below provide additional evidence for PC1's initial settings and R2's source address.

## Finding 1: A Router Was Sending Control Traffic

![R2 outbound OSPF Hello and its OSI information](../Photos/Day-03/03-ospf-hello-osi-layers.png)

Opening the PDU at R2 revealed an **OSPF HELLO**. The outbound view made it possible to trace the packet from its IP header down to the interface used to send it.

| What I checked | Value in the capture | OSI connection |
| --- | --- | --- |
| Source IP | 10.0.0.2 | Layer 3: network addressing |
| Destination IP | 224.0.0.5 | Layer 3: multicast destination |
| Source MAC | 00E0.F970.4401 | Layer 2: Ethernet sender |
| Destination MAC | 0100.5E00.0005 | Layer 2: multicast Ethernet destination |
| Outgoing interface | GigabitEthernet0/0 | Layer 1: port carrying the transmission |

Layers 4–7 are inactive for this event in the panel. This gave me a concrete example of traffic using Layers 3, 2, and 1 without a UDP or TCP header. It also showed why opening the packet details is more useful than identifying traffic by envelope color.

## Finding 2: Releasing the Address Changed PC1's Settings

![PC1 command prompt showing its initial settings, release result, and renewal attempt](../Photos/Day-03/02-pc1-dhcp-release-renew.png)

I checked PC1's configuration, released its address, and entered the renewal command:

```text
ipconfig
ipconfig /release
ipconfig /renew
```

The visible results are:

| Setting | Before release | After release |
| --- | --- | --- |
| IPv4 address | 192.168.1.10 | 0.0.0.0 |
| Subnet mask | 255.255.255.0 | 0.0.0.0 |
| Default gateway | 192.168.1.1 | 0.0.0.0 |

The screenshot ends after `ipconfig /renew` is entered. It confirms the release and renewal attempt, but does not show the resulting lease. PC1's earlier address therefore belongs to the **before-release** record.

## Connecting the DHCP Exercise to the OSI Model

DHCP provides an application-level reason to send traffic: the client needs network settings. To deliver that request, several lower-layer functions work together.

| Function | Protocol or mechanism | Layer |
| --- | --- | --- |
| Request host configuration | DHCP | 7 — Application |
| Identify the client and server services | UDP ports | 4 — Transport |
| Address the IP packet | IPv4 | 3 — Network |
| Deliver a frame on the local link | Ethernet | 2 — Data Link |
| Carry the bits between interfaces | Physical transmission | 1 — Physical |

For an initial address allocation, the usual exchange is **Discover → Offer → Request → Acknowledgment**. A client without an address normally sends its Discover from `0.0.0.0` to `255.255.255.255`, using UDP source port `68` and destination port `67`. On Ethernet, that initial broadcast uses destination MAC `FFFF.FFFF.FFFF`. Renewing an existing lease can involve a shorter exchange. These are protocol expectations; the supplied screenshots do not include a DHCP header capture. [RFC 2131](https://www.rfc-editor.org/rfc/rfc2131)

The encapsulation order is:

```text
DHCP message → UDP datagram → IPv4 packet → Ethernet frame → bits on the link
```

The distinction matters when reading the simulator: the OSPF event above verifies one set of layers, while a DHCP event would expose additional transport and application information. No separate Layer 5 or Layer 6 protocol is demonstrated in these captures.

## What the Evidence Establishes

- Simulation mode is recording events between devices.
- R2 is sending an OSPF Hello with visible IP, Ethernet, and interface information.
- PC1 initially has 192.168.1.10/24 with gateway 192.168.1.1.
- Releasing the address clears the displayed IPv4 settings.
- The renewal command has been issued; its completed result remains uncaptured.

A final `ipconfig` after renewal and a DHCP PDU screenshot would complete the client-side evidence. End-to-end connectivity is not established by these captures.

## Notes for My Next Lab

Reading the packet fields helped me connect the OSI layers to actual addresses and interfaces. The command output added a different perspective: it showed the change on the client rather than only the traffic on a link.

For future packet-analysis labs, I will capture the initial settings, the relevant packet details, and the final result. That makes it easier to explain both what I did and what the network did in response.

## Saved Evidence

| File | Contents |
| --- | --- |
| [01-simulation-mode-traffic-analysis.png](../Photos/Day-03/01-simulation-mode-traffic-analysis.png) | Topology and event list |
| [02-pc1-dhcp-release-renew.png](../Photos/Day-03/02-pc1-dhcp-release-renew.png) | PC1 settings and commands |
| [03-ospf-hello-osi-layers.png](../Photos/Day-03/03-ospf-hello-osi-layers.png) | R2 packet inspection |

The saved Packet Tracer file, `day-03-osi-model.pkt`, will be added to `Labs` when supplied.
