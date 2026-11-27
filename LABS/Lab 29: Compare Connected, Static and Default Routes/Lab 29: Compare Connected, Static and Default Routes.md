# Lab 29: Compare Connected, Static and Default Routes

## Concept

A routing table gets its entries from different sources. This lab puts all three types on one router so you can compare them.

| | **Connected (C / L)** | **Static (S)** | **Default (S\*)** |
|---|---|---|---|
| **How it appears** | Automatically, when an interface has an IP and is `up/up` | Manually typed | Manually typed |
| **Matches** | The directly attached network | One specific remote network | **Any** network (0.0.0.0/0) |
| **AD** | 0 | 1 | 1 |
| **Command** | `ip address ...` + `no shutdown` | `ip route <net> <mask> <next-hop>` | `ip route 0.0.0.0 0.0.0.0 <next-hop>` |
| **Best used for** | Local networks | Specific remote networks | Stub routers, internet exit |
| **Adapts to failure?** | Disappears if the interface goes down | No | No |

**Key ideas:**
- **C** = the network itself. **L** = the router's own IP (a /32 entry, shown on IOS 15+).
- **Priority:** the router first picks the **longest prefix match** (most specific route). If prefixes tie, it picks the **lowest AD**. So a connected or specific static route always beats the default route.
- Static and default routes depend on connected routes. If the exit interface goes down, they disappear too.

---

## Lab Design

### Topology

```
PC1 - SW1 - R1 --(Link A)-- R2 --(Link B)-- R3 - SW3 - Server
```

**R2 is the star of this lab.** It will have connected, static and default routes at the same time.

Use 3 routers (2911), 2 switches (2960), 1 PC, 1 server. You can copy your Lab 27 file and adjust it.

### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Gateway |
|--------|-----------|-----------|-------------|---------|
| PC1 | NIC | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| R1 | Gig0/0 | 192.168.1.1 | 255.255.255.0 | - |
| R1 | Gig0/1 | 10.0.0.1 | 255.255.255.252 | - |
| R2 | Gig0/0 | 10.0.0.2 | 255.255.255.252 | - |
| R2 | Gig0/1 | 10.0.0.5 | 255.255.255.252 | - |
| R3 | Gig0/0 | 10.0.0.6 | 255.255.255.252 | - |
| R3 | Gig0/1 | 8.8.8.1 | 255.255.255.0 | - |
| Server | NIC | 8.8.8.8 | 255.255.255.0 | 8.8.8.1 |

### Tasks

1. Build the topology, assign IPs, and `no shutdown` on all interfaces.
2. Run `show ip route` on R2 **before** adding any routes. Only **C** and **L** entries should appear.
3. Add the static route (LAN1) and the default route on R2.
4. Run `show ip route` on R2 again and label each line as Connected, Local, Static or Default.
5. Configure R1 and R3 so ping works end to end.
6. Ping PC1 to the Server (8.8.8.8). It should succeed.
7. Fill in this table in your notes from your R2 output:

| Destination | Route type used | Code |
|-------------|-----------------|------|
| 10.0.0.4/30 | ? | ? |
| 192.168.1.0/24 | ? | ? |
| 8.8.8.8 | ? | ? |

### Configuration

**R1:**
```
interface g0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
interface g0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown
exit
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

**R2:**
```
interface g0/0
 ip address 10.0.0.2 255.255.255.252
 no shutdown
interface g0/1
 ip address 10.0.0.5 255.255.255.252
 no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 0.0.0.0 0.0.0.0 10.0.0.6
```

**R3:**
```
interface g0/0
 ip address 10.0.0.6 255.255.255.252
 no shutdown
interface g0/1
 ip address 8.8.8.1 255.255.255.0
 no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.0.5
ip route 10.0.0.0 255.255.255.252 10.0.0.5
```

---

## Verification

| Command | What to check |
|---------|---------------|
| `show ip route` (R2, before routes) | Only `C` and `L` lines |
| `show ip route` (R2, after) | `C 10.0.0.0/30`, `L 10.0.0.2/32`, `C 10.0.0.4/30`, `L 10.0.0.5/32`, `S 192.168.1.0/24 [1/0] via 10.0.0.1`, `S* 0.0.0.0/0 [1/0] via 10.0.0.6` |
| `show ip route connected` | Only C and L entries |
| `show ip route static` | Only the S and S* entries |
| `ping 8.8.8.8` from PC1 | Replies received |
