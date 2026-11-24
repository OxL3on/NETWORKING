# Lab 25: Configure Static Routes Between Two Routers

## Concept

**Routing table basics:** A router only knows about networks it is **directly connected** to. If a destination is on a remote network, the router drops the packet unless it has a route for it.

**Static route:** A route you add manually, telling the router: *"To reach network X, send the packet to next-hop Y."*

```
ip route <destination-network> <subnet-mask> <next-hop-IP>
```

**Key rules:**
- Routing is **two-way**: R1 needs a route to R2's LAN, **and** R2 needs a route back to R1's LAN. If one is missing, ping fails (request arrives, reply is lost).
- The **next-hop** is the IP of the *other router's* interface on the shared link.
- Static routes don't adapt automatically if a link fails.

In the routing table, static routes show up with the code **S**.

---

## Lab Design

### Topology

```
PC1 ---- SW1 ---- R1 ====(serial/Gig link)==== R2 ---- SW2 ---- PC2
```

<img width="506" height="559" alt="image" src="https://github.com/user-attachments/assets/c1dfe542-899c-43ec-93d6-a1cfc9ccafbc" />

Use 2 routers (2911 or 1941), 2 switches (2960), 2 PCs. Connect R1 to R2 with a copper cross-over cable (Gig0/1 to Gig0/1).

### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Gateway |
|--------|-----------|-----------|-------------|---------|
| PC1 | NIC | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| R1 | Gig0/0 | 192.168.1.1 | 255.255.255.0 | - |
| R1 | Gig0/1 | 10.0.0.1 | 255.255.255.252 | - |
| R2 | Gig0/1 | 10.0.0.2 | 255.255.255.252 | - |
| R2 | Gig0/0 | 192.168.2.1 | 255.255.255.0 | - |
| PC2 | NIC | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |

### Tasks

1. Build the topology and assign all IPs.
2. Turn on all router interfaces (`no shutdown`).
3. **Before adding routes**, ping PC1 to PC2. It should **fail**. Take note of why.
4. Configure the static route on R1.
5. Ping again. It should **still fail** (the reply has no way back).
6. Configure the static route on R2.
7. Ping again. It should now **succeed**.

### Configuration

**R1:**
```
enable
configure terminal
interface g0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
interface g0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown
exit
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

**R2:**
```
enable
configure terminal
interface g0/0
 ip address 192.168.2.1 255.255.255.0
 no shutdown
interface g0/1
 ip address 10.0.0.2 255.255.255.252
 no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

---

## Verification

| Command | What to check |
|---------|---------------|
| `show ip route` (on R1) | Line starting with `S 192.168.2.0/24 [1/0] via 10.0.0.2` |
| `show ip route` (on R2) | Line starting with `S 192.168.1.0/24 [1/0] via 10.0.0.1` |
| `show ip interface brief` | Both interfaces `up/up` |
| `ping 192.168.2.10` from PC1 | Replies received |
| `tracert 192.168.2.10` from PC1 | Hops: 192.168.1.1, then 10.0.0.2, then 192.168.2.10 |

**Note on `[1/0]`:** `1` is the administrative distance of a static route, `0` is the metric.

## Bonus (optional)

Remove R2's route with `no ip route 192.168.1.0 255.255.255.0 10.0.0.1` and ping again. Observe the failure, then restore it. This shows why routes must exist in **both directions**.


