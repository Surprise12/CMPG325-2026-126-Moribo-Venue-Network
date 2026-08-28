# Client Requirements Analysis

## Client Overview

| Attribute | Details |
|-----------|---------|
| **Client ID** | CLI-126 |
| **Organisation** | Moribo Live Music Venue |
| **Location** | Kimberley, South Africa |
| **Industry** | Entertainment |
| **Assigned Addressing Block** | 172.30.80.0/23 |

## Functional Requirements

The Moribo Live Music Venue requires a network that supports its day‑to‑day operations. The key functional needs are:

1. **Connectivity for all venue operations** – including administrative staff, point‑of‑sale (POS) systems for ticket sales, merchandise, and concessions, as well as guest Wi‑Fi access.

2. **Inter‑VLAN Routing** – the network must enable communication between different VLANs (e.g., between POS and back‑office servers) using a Layer 3 switch with Switch Virtual Interfaces (SVIs). This is the **assigned networking challenge**.

3. **Remote Management** – the off‑site IT contractor must be able to securely access and manage network devices (switches, router) from outside the premises. This is a **design constraint**.

4. **Accommodate Change Request CR10** – four additional POS terminals are being deployed, increasing the total POS device count from two to six. The network design must seamlessly support this expansion without re‑addressing the entire network.

5. **Scalability and Performance** – the network must be reliable, with adequate capacity for current and near‑future needs.

## Technical Constraints

- Must use the assigned addressing block 172.30.80.0/23.
- Must be implemented and simulated in Cisco Packet Tracer.
- Must demonstrate successful connectivity and testing.
- Must be documented with evidence (GitHub portfolio, video demonstration).

## Business Justification

A segmented network design is essential for:
- **Security** – isolating POS traffic (payment card data) from general staff and guest traffic.
- **Performance** – reducing broadcast domains and optimising traffic flow.
- **Management** – simplifying troubleshooting and remote administration.
- **Compliance** – adhering to best practices for payment card environments (PCI DSS).

## Assumptions

- The venue has a single physical location in Kimberley.
- All end devices are stationary (wired connections) except guest Wi‑Fi.
- The IT contractor uses SSH for remote access; no VPN is required (simplified for Packet Tracer).
- Guest Wi‑Fi is isolated and does not require access to internal resources.