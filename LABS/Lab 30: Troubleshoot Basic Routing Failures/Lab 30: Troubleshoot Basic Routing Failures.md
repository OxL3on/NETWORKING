# Lab 30: Troubleshoot Basic Routing Failures

## Concept

When a ping fails, don't guess. Work through the layers in order, and stop at the first problem you find.

**The 4-step method:**

| Step | Question | Command |
|------|----------|---------|
| 1. Interfaces | Is every interface `up/up`? | `show ip interface brief` |
| 2. Addressing | Are the IPs, masks and PC gateways correct? | `show ip interface brief`, PC `ipconfig` |
| 3. Routes | Does each router have a route to the destination **and** back? | `show ip route` |
| 4. Path | Where does the packet stop? | `ping`, `tracert` |

**The most common routing failures:**

| Failure | Typical symptom |
|---------|-----------------|
| Interface shut down or cable wrong | `administratively down` or `down/down` |
| Wrong next-hop | Route missing from `show ip route` |
| Typo in network or mask | Route exists, but for the wrong network |
| Missing return route | Ping times out, `tracert` stops partway |
| Wrong PC gateway | PC can't leave its own LAN |

**Tips:**
- Ping **outward step by step**: your gateway, then the next router, then the far router, then the far PC. The first failure shows where the problem is.
- If `tracert` stops at hop N, check the route on hop N (forward) **and** on the router after it (return).
- A static route whose next-hop isn't on a connected network is **not installed**.

---

## Lab Design

### Topology

Reuse your **Lab 26** file (same topology and addressing). Save a copy as `lab30.pkt`.

```
PC1 - SW1 - R1 --(10.0.0.0/30)-- R2 --(10.0.0.4/30)-- R3 - SW3 - PC3
```

### Tasks

1. Open your working Lab 26 copy and confirm PC1 can ping PC3.
2. Inject **one fault at a time** using the table below.
3. For each fault, run the 4-step method and write down the symptom, the command that revealed it, and your fix.
4. Apply the fix, confirm the ping works, then inject the next fault.

### Faults to Inject

**Fault 1: Wrong next-hop (on R1)**
```
no ip route 192.168.3.0 255.255.255.0 10.0.0.2
ip route 192.168.3.0 255.255.255.0 10.0.0.6
```

**Fault 2: Missing return route (on R3)**
```
no ip route 192.168.1.0 255.255.255.0 10.0.0.5
```

**Fault 3: Interface shut down (on R2)**
```
interface g0/1
 shutdown
```

**Fault 4: Typo in the network address (on R2)**
```
no ip route 192.168.3.0 255.255.255.0 10.0.0.6
ip route 192.168.30.0 255.255.255.0 10.0.0.6
```

**Fault 5: Wrong gateway on PC3**
Change PC3's default gateway to `192.168.3.254`.

---

## Verification

Use this as your answer key after you try each fault yourself.

| Fault | Symptom | How to find it | Fix |
|-------|---------|----------------|-----|
| 1. Wrong next-hop | PC1 can't ping PC3 | `show ip route` on R1: no `192.168.3.0` route (10.0.0.6 is not directly connected) | Remove the bad route and add `ip route 192.168.3.0 255.255.255.0 10.0.0.2` |
| 2. Missing return route | Ping times out, `tracert` stops after 10.0.0.2 | `show ip route` on R3: no route to 192.168.1.0 | `ip route 192.168.1.0 255.255.255.0 10.0.0.5` |
| 3. Interface shut | Ping fails, `tracert` stops at R1 | `show ip interface brief` on R2: `g0/1 administratively down` | `no shutdown` on g0/1 |
| 4. Typo | PC1 can't reach PC3 | `show ip route` on R2: `192.168.30.0` instead of `192.168.3.0` | Remove the typo route and add the correct one |
| 5. Wrong PC gateway | PC3 can't leave its LAN | `ipconfig` on PC3: gateway `.254`. Ping `192.168.3.1` from PC3 fails | Set the gateway to `192.168.3.1` |

**Final check:** after fixing everything, `ping 192.168.3.10` from PC1 succeeds and `tracert` shows 192.168.1.1, 10.0.0.2, 10.0.0.6, 192.168.3.10.

