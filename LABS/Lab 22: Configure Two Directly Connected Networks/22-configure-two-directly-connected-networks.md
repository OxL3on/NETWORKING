
# Lab 22: Configure Two Directly Connected Networks

## 1. Understand the theory

A directly connected network is a network attached to one of a router's active interfaces.

For example, a router has two interfaces:

- G0/0 → `192.168.10.1/24`
- G0/1 → `192.168.20.1/24`

The router automatically recognizes both networks when the interfaces are configured and operational.

Important concepts:

- Directly Connected Route (C): A network directly connected to a router interface.
- Local Route (L): A route to the router's own interface IP address.
- Routing Table: Stores routes that the router uses to forward packets.
- Static Route: A manually configured route to a network that isn't automatically known.

You do not need static routes to communicate between these two directly connected networks.

## 2. Build the Packet Tracer topology

Use:

- 1 Router (Cisco 2911 recommended)
- 2 Switches (2960)
- 4 PCs

<img width="627" height="358" alt="image" src="https://github.com/user-attachments/assets/2dbe5748-d882-4a10-a919-449008553d75" />


Connect the router to each switch, and connect two PCs to each switch using Copper Straight-Through cables.

## 3. IP addressing plan

LAN 1

| Device      | IP address      | Gateway        |
| ----------- | --------------- | -------------- |
| Router G0/0 | `192.168.10.1`  | —              |
| PC0         | `192.168.10.10` | `192.168.10.1` |
| PC1         | `192.168.10.11` | `192.168.10.1` |

LAN 2

| Device      | IP address      | Gateway        |
| ----------- | --------------- | -------------- |
| Router G0/1 | `192.168.20.1`  | —              |
| PC2         | `192.168.20.10` | `192.168.20.1` |
| PC3         | `192.168.20.11` | `192.168.20.1` |

Subnet mask for every device: `255.255.255.0`.

## 4. Configure the router

Open Router0 → Config.

Configure:

GigabitEthernet0/0

- IP: `192.168.10.1`
- Mask: `255.255.255.0`
- Port Status: On

GigabitEthernet0/1

- IP: `192.168.20.1`
- Mask: `255.255.255.0`
- Port Status: On

## 5. Configure the PCs

Open each PC → Desktop → IP Configuration → Static.

Enter the IP addresses, subnet masks, and default gateways from the addressing tables.

## 6. Verify the routing table

This is the most important part of Lab 22.

Open Router0 → CLI and run:

```
show ip interface brief
```

Check that both interfaces are operational.

Then run:

```
show ip route
```

You should find entries similar to:

```
C 192.168.10.0/24 is directly connected, GigabitEthernet0/0
C 192.168.20.0/24 is directly connected, GigabitEthernet0/1
```

Here, `C` means Connected.

You may also see `L` routes representing the router's own interface IP addresses.

## 7. Test connectivity

From PC0's Command Prompt:

```
ping 192.168.10.11
ping 192.168.20.10
ping 192.168.20.11
```

The first tests communication inside LAN 1. The other two test communication through the router into LAN 2.

