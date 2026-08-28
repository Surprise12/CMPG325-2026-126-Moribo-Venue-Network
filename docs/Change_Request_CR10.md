# Change Request CR10 – Four Additional POS Terminals

**Change Request ID:** CR10  
**Date:** 28 August 2026  
**Requestor:** Client (Moribo Live Music Venue)  
**Impact:** Network expansion – addition of four new point‑of‑sale terminals.

## Description

The client requires the deployment of four additional POS terminals to support increased ticket and merchandise sales. These terminals must be integrated into the existing network without disrupting current operations.

## Implementation

The new POS terminals will be connected to the existing access switches (or a new access switch if needed) and assigned to the existing **VLAN 30 (POS)**. The current subnet (172.30.80.128/26) has 62 usable addresses; it currently hosts only two terminals, leaving ample capacity for the four new ones.

### Steps Taken

1. **Physical Connectivity** – The new terminals are connected to available access switch ports (e.g., FastEthernet 0/3–0/6 on L2 Switch 1 or L2 Switch 2). Ports are configured as access ports in VLAN 30.
2. **DHCP** – The existing DHCP pool for VLAN 30 (`POS_POOL`) is already configured with a range of 172.30.80.130 – 172.30.80.190, which can accommodate up to 60 terminals. No change is needed.
3. **Addressing** – Each new terminal will automatically receive an IP address from the pool, with gateway 172.30.80.129.
4. **Testing** – Connectivity tests confirm that each new terminal can ping the gateway and other devices within VLAN 30, and can reach the back‑office server if required.

### Verification

- The L3 switch’s ARP table shows the MAC addresses of all six POS terminals.
- Ping tests from a staff PC to a new POS terminal succeed (Inter‑VLAN routing works).
- The DHCP server logs show successful lease assignments for the new devices.

### No Impact on Existing Services

Because the VLAN and subnet are unchanged, the existing two POS terminals continue to operate normally. The network design’s scalability ensures that CR10 is handled without reconfiguration of core routing or addressing.

## Documentation Evidence

Screenshots of:
- DHCP leases showing new IPs.
- Ping tests from a new terminal to the gateway.
- Switchport status showing all six POS ports in VLAN 30.

*All evidence is captured in the testing/screenshots directory.*