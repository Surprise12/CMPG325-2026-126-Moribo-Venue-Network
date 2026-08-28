# Network Design Decisions & Rationale

## Topology Overview

The network adopts a **hierarchical star** topology with a single distribution/core layer (Layer 3 switch) and two access switches. This design offers:

- **Scalability** – easy addition of new access switches and end devices.
- **Manageability** – centralised routing and management on the core switch.
- **Performance** – dedicated gigabit links between distribution and access.
- **Resilience** – multiple access switches reduce single points of failure.

[Internet / Cloud]
|
[Management PC]
|
[L3 Switch - 3560] <-- Core / Distribution (SVI Routing)
/ |
/ |
[L2 SW1] [L2 SW2] [Wireless AP]
(Access) (Access) (Guest Wi-Fi)
/ | \ / |
[PCs] [POS] [PCs] [PCs] [POS] [PCs]


## VLAN Design

| VLAN ID | Name | Purpose | Subnet |
|---------|------|---------|--------|
| 10 | Management | Device management (SSH, SNMP) | 172.30.80.0/26 |
| 20 | Staff | Administrative workstations | 172.30.80.64/26 |
| 30 | POS | Point‑of‑Sale terminals | 172.30.80.128/26 |
| 40 | Guest | Public Wi‑Fi (isolated) | 172.30.80.192/27 |
| 99 | Native | Untagged traffic on trunks | N/A |

**Rationale:**
- **Management VLAN** – isolates administrative access to switches, reducing attack surface.
- **Staff VLAN** – separates office traffic from operational systems.
- **POS VLAN** – critical isolation for payment terminals; enhanced security and performance.
- **Guest VLAN** – provides internet‑only access, isolated from internal resources.
- **Native VLAN** – set to an unused VLAN (99) to prevent untagged traffic from entering user VLANs.

## Inter‑VLAN Routing (SVI)

The Layer 3 switch (Cisco 3560) will host all SVIs. Each VLAN’s SVI will serve as the default gateway for that subnet. This approach is chosen for:

- **High‑speed routing** – hardware‑based switching at near‑wire speed.
- **Simplified design** – no need for an external router.
- **Easy expansion** – adding a new VLAN is as simple as creating a new SVI.

Routing is enabled globally with `ip routing`.

## Remote Management

All network devices will have an interface on VLAN 10. Management access will be via SSH v2 (Telnet disabled). The following security measures will be implemented:

- Local user database with strong passwords (encrypted with `service password-encryption`).
- VTY lines configured to accept SSH only, with an access‑class limiting source IPs (if needed in a production environment; in Packet Tracer we will simulate with basic authentication).
- SSH version 2 enabled.

## DHCP Services

A central DHCP server will be configured on the Layer 3 switch (or a dedicated server) to assign IP addresses dynamically to end devices in each VLAN. Each VLAN will have its own DHCP pool, with the SVI as the gateway.

## Addressing & Subnetting

We used VLSM to efficiently allocate the assigned /23 block:

| VLAN | Subnet | CIDR | Usable | Why this size? |
|------|--------|------|--------|----------------|
| Management | 172.30.80.0 | /26 | 62 | Enough for current and future network devices. |
| Staff | 172.30.80.64 | /26 | 62 | Accommodates staff workstations (currently 4, scalable to ~60). |
| POS | 172.30.80.128 | /26 | 62 | Supports six POS terminals now and expansion to ~60. |
| Guest | 172.30.80.192 | /27 | 30 | Adequate for guest Wi‑Fi traffic. |

The remaining address space (172.30.80.224/27 and 172.30.81.0/24) is reserved.

## Change Request CR10 Accommodation

CR10 adds four POS terminals. The POS VLAN (/26) already has 62 usable addresses, so we simply assign the new terminals addresses within the existing DHCP scope. No subnetting changes are required.

## Testing Strategy

- **End‑to‑end connectivity** – ping from a PC in one VLAN to a device in another VLAN.
- **SVI verification** – show ip route, show ip interface brief, and ping from the switch itself.
- **Remote management** – SSH from a management PC to the L3 switch.
- **DHCP** – verify that end devices receive IPs from the correct pool.