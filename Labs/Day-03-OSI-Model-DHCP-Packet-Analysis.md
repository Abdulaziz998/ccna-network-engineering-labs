# Day 03 - OSI Model & DHCP Packet Analysis

## Overview

This lab was completed as part of my CCNA studies using Cisco Packet Tracer.

The objective was to understand how data moves through the OSI model by studying network traffic and generating DHCP communication from PC1.

I used Simulation mode to follow events between devices, inspected an OSPF Hello packet, and released PC1's IP address before issuing a renewal request. These activities connected the OSI model to the headers and commands used in a network.

---

## Network Topology

<p align="center">
  <img src="../Photos/Day-03/01-simulation-mode-traffic-analysis.png" alt="Lab topology and Simulation event list" width="1000">
</p>
<p align="center">
  <img src="../Photos/Day-03/02-pc1-dhcp-release-renew.png" alt="PC1 initial IP settings, address release, and renewal command" width="1000">
</p>
<p align="center">
  <img src="../Photos/Day-03/03-ospf-hello-osi-layers.png" alt="OSPF Hello packet at R2 showing Layers 1, 2, and 3" width="1000">
</p>

---

## Lab Objective

The goal of this lab was to:

* Observe packet encapsulation
* Study DHCP communication
* Relate network traffic to the OSI model
* Identify Ethernet, IP, and transport-layer information
* Generate DHCP traffic by releasing and renewing PC1's address
* Examine source and destination addressing

---

## Devices Used

### Client Device

* PC1

### Network Infrastructure

* Switch SW1
* Switch SW2
* Router R1
* Router R2

### Server Infrastructure

* SRV1 — server in the lab topology

---

## Network Addressing

### Local Network

```text
192.168.1.0/24
```

### Router Interfaces

```text
R1 G0/0: 192.168.1.1
R1 G0/1: 10.0.0.1
R2 G0/0: 10.0.0.2
```

### Server

```text
SRV1: 192.168.1.100
```

### PC1 Before Release

```text
IP Address:      192.168.1.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.1.1
```

### WAN Network

```text
10.0.0.0/24
```

Router and server addresses are taken from the topology labels. PC1's initial settings are visible in its command output; R2's source address is also visible in the OSPF packet.

---

## DHCP Communication Process

On PC1, the captured commands are:

```text
ipconfig
ipconfig /release
ipconfig /renew
```

The first command displays PC1's initial settings. After release, the IPv4 address, subnet mask, default gateway, and DNS server display as `0.0.0.0`. The renewal command is entered, but its completed output is not yet visible in the screenshot.

For a fresh lease, the usual DHCP sequence is **Discover → Offer → Request → Acknowledgment**. The following DHCP fields describe expected behavior; they are not captured header values from these screenshots. [DHCP specification, RFC 2131](https://www.rfc-editor.org/rfc/rfc2131)

### Layer 3 Information

An initial Discover from a client without an address normally uses:

```text
Source IP:      0.0.0.0
Destination IP: 255.255.255.255
```

The destination is an IPv4 broadcast address. PC1's earlier address, `192.168.1.10`, is its pre-release configuration; it should not be presented as the verified source of an uncaptured Discover packet.

---

### Layer 4 Information

DHCP client-to-server messages use:

```text
Protocol:         UDP
Source Port:      68
Destination Port: 67
```

These are the DHCP client and server ports. The screenshots do not yet show the DHCP PDU details needed to verify them in this run.

---

## OSI Layer Analysis

### Layer 1 - Physical

Transmits bits across the network media.

The OSPF screenshot identifies the outgoing interface as:

```text
GigabitEthernet0/0
```

This is the interface on R2 carrying the selected packet.

---

### Layer 2 - Data Link

Provides:

* MAC addressing
* Ethernet framing
* Local link delivery

The captured OSPF Ethernet header shows:

```text
Source MAC:      00E0.F970.4401
Destination MAC: 0100.5E00.0005
```

This is a multicast destination. By comparison, an initial DHCP Discover sent as an Ethernet broadcast uses destination `FFFF.FFFF.FFFF`; that DHCP frame is not shown in the supplied PDU screenshot.

---

### Layer 3 - Network

Provides IP addressing and packet forwarding between networks.

The selected OSPF Hello at R2 shows:

```text
Source IP:      10.0.0.2
Destination IP: 224.0.0.5
Message:        OSPF HELLO
```

This is a captured Layer 3 control packet. The PDU panel describes multicast transmission from R2.

---

### Layer 4 - Transport

Uses transport protocols and port numbers to deliver data to the appropriate service.

For the DHCP client request studied in this exercise:

```text
Protocol:             UDP
Client Source Port:   68
Server Destination Port: 67
```

The selected OSPF event has Layer 4 inactive in the panel. Its packet details should not be interpreted as a UDP or DHCP capture.

---

### Layer 7 - Application

Provides application-level network services. DHCP supplies host configuration.

```text
DHCP Discover: client searches for a DHCP server
```

This describes the application message to inspect after generating DHCP traffic. A readable Discover PDU is still needed to document its actual fields in this lab.

Layers 5 and 6 are part of the OSI model, but no separate session- or presentation-layer protocol is demonstrated in these captures.

---

## Packet Encapsulation

A DHCP message is carried by lower-layer protocols before transmission:

```text
DHCP Application Data
↓
UDP Header
↓
IPv4 Header
↓
Ethernet Header and Trailer
↓
Physical Transmission
```

This process is encapsulation. The captured OSPF event illustrates a different case: its active outbound layers are Layers 3, 2, and 1.

---

## Key Concepts Learned

### Broadcast Communication

A DHCP client without an address can broadcast to locate a server on its local network. Broadcast and multicast addresses serve different purposes; the captured OSPF Hello uses multicast.

### DHCP Process

DHCP can supply:

* IP address
* Subnet mask
* Default gateway
* DNS server information

The gateway supports communication beyond the local subnet, and DNS supports name resolution. Neither is required for every local IP exchange. A renewal of an existing lease may use a shorter exchange than fresh allocation.

### OSI Model Application

Different events involve different protocols and layers. The OSPF capture provides direct evidence of Layers 1–3. DHCP adds application and transport information, which should be checked in its own PDU details.

---

## Skills Practiced

* OSI model analysis
* DHCP release and renewal commands
* Packet encapsulation concepts
* Ethernet and IPv4 header inspection
* OSPF Hello packet inspection
* UDP and broadcast fundamentals
* Cisco Packet Tracer Simulation mode
* Distinguishing observed results from expected protocol behavior

---

## What I Learned

This lab helped connect networking theory to visible packet information. Inspecting the OSPF Hello showed how a Layer 3 packet is carried inside an Ethernet frame and sent through a physical interface.

Releasing PC1's address showed the immediate change in its IP settings. Issuing the renewal command provided the next step for studying DHCP traffic and application-layer encapsulation.

The saved evidence confirms the initial client settings, successful release, renewal attempt, and OSPF packet details. The completed renewal output and DHCP PDU details remain to be captured. The completed Packet Tracer file can be added as `Labs/day-03-osi-model.pkt` when supplied.
