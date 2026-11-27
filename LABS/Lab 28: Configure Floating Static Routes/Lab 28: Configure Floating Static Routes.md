# Lab 28: Configure Floating Static Routes

## Concept

**Problem:** A static route doesn't adapt. If the link fails, the route disappears and there is no automatic backup unless you configure one.

**Floating static route:** A backup static route with a **higher administrative distance (AD)** than the main route. It "floats" unused in the background until the main route disappears.

```
ip route <network> <mask> <next-hop> <AD>
```

**Key ideas:**
- Lower AD = more trusted. Default static AD is **1**.
- Give the backup route a higher AD (e.g. **5**). The router installs only the **lowest-AD** route, so the backup stays **hidden** from the routing table.
- When the primary link goes down, the primary route is removed and the backup route appears.
- When the primary link comes back, the primary route returns and the backup hides again.
- **Limitation:** It only reacts when the **interface goes down**. If the failure is further away and your interface stays up, the primary route stays and traffic is lost.

| Route type | AD |
|------------|----|
| Connected | 0 |
| Static (default) | 1 |
| Floating static (this lab) | 5 |

---

## Lab Design

### Topology

```
                  Primary (10.0.0.0/30)
PC1 - SW1 - R1 ==========================  R2 - SW2 - PC2
               ========================== 
                  Backup (10.0.1.0/30)
```

<img width="755" height="505" alt="image" src="https://github.com/user-attachments/assets/e7d02956-dde5-4b88-82f0-f80060d4f12e" />

Use 2 routers (2911), 2 switches (2960), 2 PCs. Connect R1 and R2 with **two** copper cross-over cables (Gig0/1 to Gig0/1 as primary, Gig0/2 to Gig0/2 as backup).

### Addressing Table

| Device | Interface | IP Address | Subnet Mask | Gateway |
|--------|-----------|-----------|-------------|---------|
| PC1 | NIC | 192.168.1.10 | 255.255.255.0 | 192.168.1.1 |
| R1 | Gig0/0 | 192.168.1.1 | 255.255.255.0 | - |
| R1 | Gig0/1 (primary) | 10.0.0.1 | 255.255.255.252 | - |
| R1 | Gig0/2 (backup) | 10.0.1.1 | 255.255.255.252 | - |
| R2 | Gig0/0 | 192.168.2.1 | 255.255.255.0 | - |
| R2 | Gig0/1 (primary) | 10.0.0.2 | 255.255.255.252 | - |
| R2 | Gig0/2 (backup) | 10.0.1.2 | 255.255.255.252 | - |
| PC2 | NIC | 192.168.2.10 | 255.255.255.0 | 192.168.2.1 |

### Tasks

1. Build the topology, assign IPs, and `no shutdown` on all interfaces.
2. Configure the **primary** static route on both routers (default AD 1).
3. Configure the **floating** static route on both routers (AD 5) via the backup link.
4. Run `show ip route` and confirm only the primary route is shown.
5. Start a continuous ping from PC1 to PC2 and `tracert` to see the path.
6. Shut down the primary link on R1 and watch the backup take over.
7. Bring the primary link back and watch traffic return.

### Configuration

**R1:**
```
interface g0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
interface g0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown
interface g0/2
 ip address 10.0.1.1 255.255.255.252
 no shutdown
exit
ip route 192.168.2.0 255.255.255.0 10.0.0.2
ip route 192.168.2.0 255.255.255.0 10.0.1.2 5
```

**R2:**
```
interface g0/0
 ip address 192.168.2.1 255.255.255.0
 no shutdown
interface g0/1
 ip address 10.0.0.2 255.255.255.252
 no shutdown
interface g0/2
 ip address 10.0.1.2 255.255.255.252
 no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 192.168.1.0 255.255.255.0 10.0.1.1 5
```

**Failover test (on R1):**
```
interface g0/1
 shutdown
```
**Restore:**
```
interface g0/1
 no shutdown
```

---

## Verification

| Step | Command | What to check |
|------|---------|---------------|
| Normal state | `show ip route` (R1) | `S 192.168.2.0/24 [1/0] via 10.0.0.2` only. No `[5/0]` route is visible. |
| Normal state | `tracert 192.168.2.10` (PC1) | Hops: 192.168.1.1, **10.0.0.2**, 192.168.2.10 |
| Config check | `show running-config \| include ip route` | Both routes are listed |
| After shutdown | `show ip route` (R1) | `S 192.168.2.0/24 [5/0] via 10.0.1.2` appears |
| After shutdown | `tracert 192.168.2.10` (PC1) | Hops: 192.168.1.1, **10.0.1.2**, 192.168.2.10 |
| After restore | `show ip route` (R1) | Back to `[1/0] via 10.0.0.2` |

**Tip:** You may lose a few pings during the switch. This is normal while the routing table updates.
