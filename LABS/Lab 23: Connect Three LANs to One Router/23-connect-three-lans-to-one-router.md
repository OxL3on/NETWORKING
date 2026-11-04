

# Lab 23: Connect Three LANs to One Router

## Step 1 — Understand the objective

A router can connect multiple LANs using multiple network interfaces.

Each interface belongs to a different IP network and acts as the default gateway for that LAN.

For this lab, we'll use:

- 1 Router
- 3 Switches
- 6 PCs (2 per LAN)

## Step 2 — Build the topology

<img width="616" height="308" alt="image" src="https://github.com/user-attachments/assets/5ae980fc-feba-4e15-866a-c1f31bc94ddd" />


Router recommendation: Use a Cisco 2911 router. It has three Gigabit Ethernet interfaces: G0/0, G0/1 and G0/2.

Connect each router interface to a separate 2960 switch. Connect two PCs to each switch.

Use Copper Straight-Through cables.

## Step 3 — IP addressing plan

LAN 1

| Device      | IP address      | Gateway        |
| ----------- | --------------- | -------------- |
| Router G0/0 | `192.168.10.1`  | —              |
| PC0         | `192.168.10.10` | `192.168.10.1` |
| PC1         | `192.168.10.20` | `192.168.10.1` |

LAN 2

| Device      | IP address      | Gateway        |
| ----------- | --------------- | -------------- |
| Router G0/1 | `192.168.20.1`  | —              |
| PC2         | `192.168.20.10` | `192.168.20.1` |
| PC3         | `192.168.20.20` | `192.168.20.1` |

LAN 3

| Device      | IP address      | Gateway        |
| ----------- | --------------- | -------------- |
| Router G0/2 | `192.168.30.1`  | —              |
| PC4         | `192.168.30.10` | `192.168.30.1` |
| PC5         | `192.168.30.20` | `192.168.30.1` |

Subnet mask for all devices: `255.255.255.0`.

## Step 4 — Configure the router

Open Router0 → Config.

Configure each interface:

| Interface          | IP address     | Subnet mask     |
| ------------------ | -------------- | --------------- |
| GigabitEthernet0/0 | `192.168.10.1` | `255.255.255.0` |
| GigabitEthernet0/1 | `192.168.20.1` | `255.255.255.0` |
| GigabitEthernet0/2 | `192.168.30.1` | `255.255.255.0` |

Turn Port Status: On for all three interfaces.

## Step 5 — Configure the PCs

For each PC:

1. Open the PC.
2. Select Desktop → IP Configuration.
3. Select Static.
4. Enter its IP address, subnet mask and default gateway from the tables above.

Wait until all links become green.

## Step 6 — Verify the routing table

Open Router0 → CLI.

Run:

```
show ip interface brief
```

Check that all three interfaces are up.

Then:

```
show ip route
```

You should see three directly connected networks:

```
C 192.168.10.0/24
C 192.168.20.0/24
C 192.168.30.0/24
```

You should also see three local routes (`L`), one for each router interface IP.

## Step 7 — Test connectivity

From PC0, open Command Prompt and test:

```
ping 192.168.10.20
ping 192.168.20.10
ping 192.168.20.20
ping 192.168.30.10
ping 192.168.30.20
```

All should succeed after the network is configured correctly.
