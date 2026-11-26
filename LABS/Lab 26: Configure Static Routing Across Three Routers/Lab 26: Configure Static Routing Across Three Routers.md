# Lab 26: Configure Static Routing Across Three Routers

## Concept

**The problem:** In Lab 25, each router was directly connected to the other. With three routers in a line, the **middle router** is the only one that knows both sides, and the **end routers** know nothing about the far LAN.

**Rule:** Every router needs a route to **every network it is not directly connected to.**

**How to count the routes needed:**
```
Routes needed = (total networks) - (directly connected networks)
```

**Key ideas:**
- Each static route points to the **next-hop**, which is always a router on a **directly connected** link, never a router further away.
- The end routers must go *through* the middle router to reach the far side.
- Routes must exist in **both directions**, as in Lab 25.

---

## Lab Design

### Topology

```
PC1 --- SW1 --- R1 ===== R2 ===== R3 --- SW3 --- PC3
                         |
                        (R2 has no LAN in this lab)
```

<img width="436" height="510" alt="image" src="https://github.com/user-attachments/assets/777c56e1-71cc-4155-a954-10b230561df5" />

Simplified line:

```
PC1 - SW1 - R1 --(Net A)-- R2 --(Net B)-- R3 - SW3 - PC3
```

Use 3 routers (2911), 2 switches (2960), 2 PCs. Connect routers with copper cross-over cables.

### Networks

| Network | Address | Purpose |
|---------|---------|---------|
| LAN1 | 192.168.1.0/24 | PC1 LAN |
| Link A | 10.0.0.0/30 | R1 to R2 |
| Link B | 10.0.0.4/30 | R2 to R3 |
| LAN3 | 192.168.3.0/24 | PC3 LAN |

### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Gateway |
|--------|-----------|-----------|-------------|---------|
| PC1 | NIC | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| R1 | Gig0/0 | 192.168.1.1 | 255.255.255.0 | - |
| R1 | Gig0/1 | 10.0.0.1 | 255.255.255.252 | - |
| R2 | Gig0/0 | 10.0.0.2 | 255.255.255.252 | - |
| R2 | Gig0/1 | 10.0.0.5 | 255.255.255.252 | - |
| R3 | Gig0/0 | 10.0.0.6 | 255.255.255.252 | - |
| R3 | Gig0/1 | 192.168.3.1 | 255.255.255.0 | - |
| PC3 | NIC | 192.168.3.10 | 255.255.255.0 | 192.168.3.1 |

### Routes Needed

| Router | Missing networks | Static routes needed |
|--------|------------------|----------------------|
| R1 | Link B, LAN3 | 2 |
| R2 | LAN1, LAN3 | 2 |
| R3 | LAN1, Link A | 2 |

### Tasks

1. Build the topology and assign all IPs.
2. Turn on all interfaces.
3. Ping PC1 to PC3. It should **fail**.
4. Configure static routes on R1, then R3, then R2.
5. Ping again. It should now **succeed**.

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
ip route 10.0.0.4 255.255.255.252 10.0.0.2
ip route 192.168.3.0 255.255.255.0 10.0.0.2
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
ip route 192.168.3.0 255.255.255.0 10.0.0.6
```

**R3:**
```
interface g0/0
 ip address 10.0.0.6 255.255.255.252
 no shutdown
interface g0/1
 ip address 192.168.3.1 255.255.255.0
 no shutdown
exit
ip route 10.0.0.0 255.255.255.252 10.0.0.5
ip route 192.168.1.0 255.255.255.0 10.0.0.5
```

---

## Verification

| Command | What to check |
|---------|---------------|
| `show ip route` (R1) | Two `S` routes via `10.0.0.2` |
| `show ip route` (R2) | `S` routes to 192.168.1.0/24 via 10.0.0.1 and 192.168.3.0/24 via 10.0.0.6 |
| `show ip route` (R3) | Two `S` routes via `10.0.0.5` |
| `ping 192.168.3.10` from PC1 | Replies received |
| `tracert 192.168.3.10` from PC1 | Hops: 192.168.1.1, 10.0.0.2, 10.0.0.6, 192.168.3.10 |

