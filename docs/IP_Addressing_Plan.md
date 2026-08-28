# IP Addressing Plan

## Assigned Block: 172.30.80.0/23

The block is subnetted as follows:

| VLAN | Network Address | CIDR | Usable Range | Broadcast | Gateway (SVI) |
|------|-----------------|------|--------------|-----------|---------------|
| VLAN 10 (Management) | 172.30.80.0 | /26 | 172.30.80.1 – 172.30.80.62 | 172.30.80.63 | 172.30.80.1 |
| VLAN 20 (Staff) | 172.30.80.64 | /26 | 172.30.80.65 – 172.30.80.126 | 172.30.80.127 | 172.30.80.65 |
| VLAN 30 (POS) | 172.30.80.128 | /26 | 172.30.80.129 – 172.30.80.190 | 172.30.80.191 | 172.30.80.129 |
| VLAN 40 (Guest) | 172.30.80.192 | /27 | 172.30.80.193 – 172.30.80.222 | 172.30.80.223 | 172.30.80.193 |

**Reserved:** 172.30.80.224/27 and 172.30.81.0/24 for future use.

## Static Assignments

### Network Infrastructure (VLAN 10)

| Device | Interface | IP Address |
|--------|-----------|------------|
| L3 Switch (3560) | VLAN 10 SVI | 172.30.80.1/26 |
| L2 Switch 1 (2960) | VLAN 10 | 172.30.80.2/26 |
| L2 Switch 2 (2960) | VLAN 10 | 172.30.80.3/26 |
| Management PC | NIC | 172.30.80.10/26 |
| DHCP Server (if dedicated) | NIC | 172.30.80.11/26 |

### Staff VLAN 20 (DHCP Range: 172.30.80.70 – 172.30.80.120)

- Default Gateway: 172.30.80.65
- Static staff PCs may be assigned from .66 to .69 if needed.

### POS VLAN 30 (DHCP Range: 172.30.80.130 – 172.30.80.190)

- Default Gateway: 172.30.80.129
- Six POS terminals will receive addresses from this pool. Two existing + four new (CR10).

### Guest VLAN 40 (DHCP Range: 172.30.80.195 – 172.30.80.222)

- Default Gateway: 172.30.80.193

## DHCP Configuration Summary

| VLAN | Pool Name | Network | Gateway | DNS (optional) |
|------|-----------|---------|---------|----------------|
| 10 | MGMT_POOL | 172.30.80.0 /26 | 172.30.80.1 | - |
| 20 | STAFF_POOL | 172.30.80.64 /26 | 172.30.80.65 | 8.8.8.8 |
| 30 | POS_POOL | 172.30.80.128 /26 | 172.30.80.129 | - |
| 40 | GUEST_POOL | 172.30.80.192 /27 | 172.30.80.193 | 8.8.8.8 |