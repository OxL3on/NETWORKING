# Lab 27: Configure a Default Route

## Concept

**Default route:** A "catch-all" route that says: *"If I have no specific route for a destination, send the packet here."* It is also called the **gateway of last resort**.

```
ip route 0.0.0.0 0.0.0.0 <next-hop-IP>
```

`0.0.0.0/0` matches **every** IP address, but it is the **least specific** match, so the router only uses it when nothing better exists (longest-prefix match).

**Where it is used:**
- **Stub routers** (only one way out): instead of many static routes, use one default route.
- **Internet edge:** The router sends all unknown traffic to the ISP.

**Key ideas:**
- Fewer commands than static routes: 1 default route replaces many.
- The router still needs **connected routes** for its own networks.
- The return path still matters: the other side needs a route back (static or default).
- In the routing table, a default route shows as **S\*** and the router displays `Gateway of last resort is ... to network 0.0.0.0`.

---

## Lab Design

### Topology

```
PC1 - SW1 - R1 --(Link)-- R2 - SW2 - PC2
                           |
                        (ISP/Internet)
                           |
                         Cloud/Server
```

Simplified: R1 is a **stub router** (one exit). R2 is the "ISP side" and has the full routes.

```
PC1 - SW1 - R1 ---- R2 - SW2 - PC2
                     |
                    R3 (ISP) - SW3 - Server
```

Use 3 routers (2911), 3 switches (2960), 2 PCs, 1 server.

### Networks

| Network | Address | Purpose |
|---------|---------|---------|
| LAN1 | 192.168.1.0/24 | PC1 LAN (behind R1) |
| Link A | 10.0.0.0/30 | R1 to R2 |
| LAN2 | 192.168.2.0/24 | PC2 LAN |
| Link B | 10.0.0.4/30 | R2 to R3 (ISP) |
| Internet | 8.8.8.0/24 | Server (simulated internet) |

### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Gateway |
|--------|-----------|-----------|-------------|---------|
| PC1 | NIC | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| R1 | Gig0/0 | 192.168.1.1 | 255.255.255.0 | - |
| R1 | Gig0/1 | 10.0.0.1 | 255.255.255.252 | - |
| R2 | Gig0/0 | 10.0.0.2 | 255.255.255.252 | - |
| R2 | Gig0/1 | 10.0.0.5 | 255.255.255.252 | - |
| R2 | Gig0/2 | 192.168.2.1 | 255.255.255.0 | - |
| R3 | Gig0/0 | 10.0.0.6 | 255.255.255.252 | - |
| R3 | Gig0/1 | 8.8.8.1 | 255.255.255.0 | - |
| PC2 | NIC | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |
| Server | NIC | 8.8.8.8 | 255.255.255.0 | 8.8.8.1 |

> R2 needs 3 interfaces. If your router has only 2 Gig ports, add an HWIC module or use a 2911 (it has 3).

### Tasks

1. Build the topology and assign all IPs, then `no shutdown` on all interfaces.
2. On **R1**, configure **one default route** toward R2 (instead of listing each network).
3. On **R2**, configure static routes to LAN1 (via R1) and a **default route** toward R3 (ISP).
4. On **R3**, configure static routes back to LAN1, LAN2 and Link A (via R2).
5. Ping PC1 to PC2 and PC1 to the Server (8.8.8.8). Both should succeed.

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
interface g0/2
 ip address 192.168.2.1 255.255.255.0
 no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 0.0.0.0 0.0.0.0 10.0.0.6
```

**R3 (ISP):**
```
interface g0/0
 ip address 10.0.0.6 255.255.255.252
 no shutdown
interface g0/1
 ip address 8.8.8.1 255.255.255.0
 no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.0.5
ip route 192.168.2.0 255.255.255.0 10.0.0.5
ip route 10.0.0.0 255.255.255.252 10.0.0.5
```

---

## Verification

| Command | What to check |
|---------|---------------|
| `show ip route` (R1) | `Gateway of last resort is 10.0.0.2` and a line `S* 0.0.0.0/0 [1/0] via 10.0.0.2` |
| `show ip route` (R2) | One `S` route to 192.168.1.0/24 and one `S*` default route via 10.0.0.6 |
| `ping 192.168.2.10` from PC1 | Replies (R1 uses default route, R2 uses connected route) |
| `ping 8.8.8.8` from PC1 | Replies (R1 default, then R2 default, then R3 connected) |
| `tracert 8.8.8.8` from PC1 | Hops: 192.168.1.1, 10.0.0.2, 10.0.0.6, 8.8.8.8 |
