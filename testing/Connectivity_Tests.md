# Connectivity Test Plan & Results

## Test Objective

Verify that all end devices can communicate as intended, both within their VLAN and across VLANs (via Inter‑VLAN routing). Also verify remote management access.

## Test Environment

- Packet Tracer simulation with devices configured as per design.
- Devices: Staff PC1 (VLAN 20), POS Terminal 1 (VLAN 30), Management PC (VLAN 10), Guest device (VLAN 40).

## Test Cases

### 1. Intra‑VLAN Connectivity

| Source | Destination | Expected Result | Result |
|--------|-------------|-----------------|--------|
| Staff PC1 (VLAN20) | Staff PC2 (VLAN20) | Ping successful | ✔ Pass |
| POS T1 (VLAN30) | POS T6 (VLAN30) | Ping successful | ✔ Pass |
| Management PC (VLAN10) | L3 Switch (VLAN10) | Ping successful | ✔ Pass |

### 2. Inter‑VLAN Connectivity

| Source | Destination | Expected Result | Result |
|--------|-------------|-----------------|--------|
| Staff PC1 (VLAN20) | POS T1 (VLAN30) | Ping successful | ✔ Pass |
| POS T1 (VLAN30) | Staff PC1 (VLAN20) | Ping successful | ✔ Pass |
| Management PC (VLAN10) | Staff PC1 (VLAN20) | Ping successful | ✔ Pass |
| Guest device (VLAN40) | Staff PC1 (VLAN20) | Ping should fail | ✔ Pass (blocked) |
| Guest device (VLAN40) | Internet (8.8.8.8) | Ping successful | ✔ Pass |

### 3. Remote Management (SSH)

| Source | Destination | Action | Expected Result | Result |
|--------|-------------|--------|-----------------|--------|
| Management PC (VLAN10) | L3 Switch (172.30.80.1) | SSH session | Successful login | ✔ Pass |
| Management PC (VLAN10) | L2 Switch1 (172.30.80.2) | SSH session | Successful login | ✔ Pass |
| Management PC (VLAN10) | L2 Switch2 (172.30.80.3) | SSH session | Successful login | ✔ Pass |

### 4. DHCP Verification

| Device | VLAN | Received IP | Correct Pool? | Result |
|--------|------|-------------|---------------|--------|
| Staff PC1 | 20 | 172.30.80.70 | Yes | ✔ Pass |
| POS T3 (new) | 30 | 172.30.80.131 | Yes | ✔ Pass |
| Guest device | 40 | 172.30.80.195 | Yes | ✔ Pass |

## Test Summary

All critical tests passed. The network meets the client requirements for connectivity, inter‑VLAN routing, remote management, and CR10 expansion.

## Screenshots

Screenshots are available in the `testing/screenshots/` directory, showing ping outputs, SSH sessions, and DHCP bindings.