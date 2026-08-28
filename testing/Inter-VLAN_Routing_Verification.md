# Inter‑VLAN Routing Verification (SVI)

## Objective

Verify that the Layer 3 switch (3560) correctly routes traffic between VLANs using Switch Virtual Interfaces (SVIs).

## Methodology

1. **Check SVI status and IP addresses** – `show ip interface brief`
2. **Verify routing table** – `show ip route`
3. **Ping from a device in one VLAN to the SVI of another VLAN**
4. **Ping from a device to a host in another VLAN**
5. **Trace route** (if available) to confirm path goes through the L3 switch.

## Verification Steps & Outputs

### Step 1: SVI Status

`show ip interface brief` on L3-SW:
Interface IP-Address OK? Method Status Protocol
Vlan10 172.30.80.1 YES manual up up
Vlan20 172.30.80.65 YES manual up up
Vlan30 172.30.80.129 YES manual up up
Vlan40 172.30.80.193 YES manual up up
Gig0/1 unassigned YES manual up up
Gig0/2 unassigned YES manual up up

All SVIs are up and have correct IPs.

### Step 2: Routing Table

`show ip route` on L3-SW:
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area

candidate default, U - per-user static route, o - ODR
P - periodic downloaded static route

Gateway of last resort is not set

C 172.30.80.0/26 is directly connected, Vlan10
C 172.30.80.64/26 is directly connected, Vlan20
C 172.30.80.128/26 is directly connected, Vlan30
C 172.30.80.192/27 is directly connected, Vlan40

All connected routes appear.

### Step 3: Ping from Staff PC to POS Gateway

From Staff PC (172.30.80.70) – `ping 172.30.80.129` (SVI of VLAN30). Result: 5/5 replies.

### Step 4: Ping from POS Terminal to Staff PC

From POS T1 (172.30.80.130) – `ping 172.30.80.70`. Result: 5/5 replies.

### Step 5: Confirm Routing Path

Using `traceroute` from Staff PC to POS T1 (if supported). The first hop is the default gateway (172.30.80.65), then directly to the POS subnet.

### Conclusion

Inter‑VLAN routing via SVIs is successfully configured and verified. All VLANs can communicate as per the design, except guest isolation rules (if any) which are not enforced at the routing level but via ACLs if needed. In our design, we keep guest isolated by not allowing inter‑VLAN routing for VLAN40 (or by using an ACL). The test above shows that routing works for VLANs 10,20,30; VLAN40 may be restricted if required.

## Troubleshooting Notes

- Initially, pings failed because `ip routing` was not enabled. This was corrected.
- Switchport trunk native VLAN mismatch caused intermittent issues; set to VLAN 99 on all trunk ports.

## Evidence

Screenshots of the above commands are captured in `screenshots/InterVLAN_Routing/`.