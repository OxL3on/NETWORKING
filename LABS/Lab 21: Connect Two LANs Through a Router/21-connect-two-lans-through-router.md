# Lab 21: Connect Two LANs Through a Router

## Objective

Understand how a router connects two different LANs and forwards packets between them.

## 1. Why Do We Need a Router?

A switch connects devices within the same LAN. However, communication between different IP networks requires a Layer 3 device, such as a router.

A router forwards IP packets between different networks using its routing table.

## 2. Example Network Topology

Two LANs connected through one router:

**LAN 1:**
- Network: `192.168.1.0/24`
- PC0: `192.168.1.10`
- Router interface: `192.168.1.1`

**LAN 2:**
- Network: `192.168.2.0/24`
- PC1: `192.168.2.10`
- Router interface: `192.168.2.1`

Both LANs use subnet mask `255.255.255.0`.

## 3. Default Gateway

A default gateway is the router interface that a device uses to reach destinations outside its local network.

Example:

- PC0 gateway: `192.168.1.1`
- PC1 gateway: `192.168.2.1`

When a PC sends data to another network, it forwards the Ethernet frame to its default gateway.

## 4. How Communication Works Between Two LANs

Suppose PC0 wants to ping PC1 (`192.168.2.10`).

1. PC0 checks whether the destination IP belongs to its local subnet.
2. Since PC1 belongs to a different subnet, PC0 sends the packet to its default gateway (`192.168.1.1`).
3. PC0 uses ARP to discover the gateway's MAC address if it is not already cached.
4. The router receives the packet and checks its routing table.
5. The router identifies the destination network and forwards the packet through its interface connected to LAN 2.
6. The router uses ARP to discover PC1's MAC address if necessary.
7. PC1 receives the packet and sends an ICMP Echo Reply.
8. The router forwards the reply back to PC0.

## 5. Router Interfaces

Each router interface connected to a LAN needs an IP address belonging to that LAN's subnet.

Example:

| Router Interface | IP Address | Connected Network |
|---|---|---|
| G0/0 | `192.168.1.1/24` | `192.168.1.0/24` |
| G0/1 | `192.168.2.1/24` | `192.168.2.0/24` |

Router interfaces must be enabled and correctly configured for communication.

## 6. Routing Table

A routing table contains information about networks a router can reach and how to reach them.

When router interfaces are configured with IP addresses and enabled, their directly connected networks are automatically added to the routing table.

The router uses this information to forward packets toward their destination networks.

## 7. Important Concepts

- **Router:** Connects different IP networks.
- **LAN:** A local area network.
- **Default Gateway:** The router interface used to reach external networks.
- **Routing Table:** Contains routes used to forward packets.
- **ARP:** Resolves local IPv4 addresses to MAC addresses.
- **ICMP:** Used by ping to test network connectivity.
- **Different Subnets:** Devices in different IP networks communicate through a router or another Layer 3 device.

A router connects different LANs and forwards IP packets between them. Each PC needs the correct default gateway to communicate with devices outside its own subnet.
