# Moribo Live Music Venue — Network Design & Implementation

**Project ID:** CMPG325-2026-126  
**Student:** SELOWA, S (45192472)  
**Client:** Moribo Live Music Venue (Kimberley)  
**Industry:** Entertainment  
**Assigned Addressing Block:** 172.30.80.0/23  

## Project Overview

This project involves the design, simulation, and implementation of a computer network for the Moribo Live Music Venue in Kimberley. The network is built in Cisco Packet Tracer and demonstrates **Inter-VLAN Routing** using a Layer 3 switch with Switch Virtual Interfaces (SVIs). The design accommodates the client change request (CR10) to deploy four additional point-of-sale terminals, and includes remote management capabilities for an off-site IT contractor.

## Key Features

- **Inter-VLAN Routing** – Layer 3 switch (Cisco 3560) using SVIs for high‑performance routing between VLANs.
- **VLAN Segmentation** – Four isolated VLANs for Management, Staff, POS, and Guest traffic.
- **Remote Management** – SSH v2 access for the off‑site IT contractor, with management interfaces placed on a dedicated VLAN.
- **Change Request CR10** – Expanded POS VLAN to support six terminals (two existing + four new).
- **DHCP Services** – Dynamic IP assignment for end devices in each VLAN.
- **Scalable Addressing** – VLSM used to efficiently utilise the assigned /23 block.

## Addressing Block & Subnetting

| VLAN | Subnet | CIDR | Usable Hosts | Gateway (SVI) |
|------|--------|------|--------------|---------------|
| Management (VLAN 10) | 172.30.80.0 | /26 | 62 | 172.30.80.1 |
| Staff (VLAN 20) | 172.30.80.64 | /26 | 62 | 172.30.80.65 |
| POS (VLAN 30) | 172.30.80.128 | /26 | 62 | 172.30.80.129 |
| Guest (VLAN 40) | 172.30.80.192 | /27 | 30 | 172.30.80.193 |

*Remaining address space reserved for future expansion.*

## Technical Stack

- **Simulation Tool:** Cisco Packet Tracer 8.2.x
- **Switches:** Cisco 3560-24PS (Layer 3 distribution), Cisco 2960-24TT (Layer 2 access)
- **Protocols:** 802.1Q trunking, SSH v2, DHCP, IPv4
- **End Devices:** PCs, POS terminals, wireless access point (guest Wi‑Fi)

## Repository Structure
├── README.md
├── docs/
│ ├── Client_Requirements.md
│ ├── Network_Design.md
│ ├── IP_Addressing_Plan.md
│ └── Change_Request_CR10.md
├── topology/
│ ├── Physical_Topology.png
│ ├── Logical_Topology.png
│ └── Topology_Diagrams.vsdx
├── packet-tracer/
│ └── moribo_venue_network.pkt
├── configurations/
│ ├── L3_Switch_Config.txt
│ ├── L2_Switch1_Config.txt
│ ├── L2_Switch2_Config.txt
│ └── device_configs/
├── testing/
│ ├── Connectivity_Tests.md
│ ├── Inter-VLAN_Routing_Verification.md
│ └── screenshots/
└── deliverables/
├── Milestone1_Client_Design_Review.pdf
├── Milestone2_Implementation.pdf
└── Final_Submission.pdf

## Milestones

- **Milestone 1:** Client Design Review – 28 August 2026
- **Milestone 2:** Implementation & Testing – 2 October 2026
- **Final Submission:** 16 October 2026

## Author

SELOWA, S  
Student Number: 45192472  
North‑West University – CMPG325 Computer Networks