# Lab 14: Build Multiple Subnets

## Objective

Divide `172.16.10.0/24` into four equal-sized IPv4 subnets, configure a router and four LANs in Cisco Packet Tracer, and verify connectivity within and between subnets.

---

## Part 1: Calculate the Four Subnets

### Step 1: Calculate borrowed bits and the new prefix

Original network: `172.16.10.0/24`

Required subnets: `4`

Use the smallest number of borrowed bits that creates four subnets:

- `2^1 = 2` subnets — not enough
- `2^2 = 4` subnets — enough

Borrowed bits = `2`

New prefix = `24 + 2 = /26`

### Step 2: Find the subnet mask and block size

A `/26` subnet has the mask:

- Binary: `11111111.11111111.11111111.11000000`
- Decimal: `255.255.255.192`

The interesting octet is the fourth octet.

`Block size = 256 - 192 = 64`

Therefore, the subnet network addresses increase by 64 in the fourth octet.

### Step 3: Calculate total and usable addresses per subnet

Host bits = `32 - 26 = 6`

Total addresses per subnet:

`2^6 = 64`

Conventional usable host addresses:

`64 - 2 = 62`

The network address and broadcast address are excluded from the usable-host count. A router gateway address is still a usable host address.

### Step 4: Calculate the network and broadcast addresses

The four fourth-octet ranges are:

- `0–63`
- `64–127`
- `128–191`
- `192–255`

| Subnet | Network address | Broadcast address |
|---|---|---|
| 1 | `172.16.10.0/26` | `172.16.10.63` |
| 2 | `172.16.10.64/26` | `172.16.10.127` |
| 3 | `172.16.10.128/26` | `172.16.10.191` |
| 4 | `172.16.10.192/26` | `172.16.10.255` |

### Step 5: Calculate the usable host range

- First usable host = network address + 1
- Last usable host = broadcast address - 1

| Subnet | Network address | First usable host | Last usable host | Broadcast address | Total addresses | Usable hosts |
|---|---|---|---|---|---:|---:|
| 1 | `172.16.10.0` | `172.16.10.1` | `172.16.10.62` | `172.16.10.63` | 64 | 62 |
| 2 | `172.16.10.64` | `172.16.10.65` | `172.16.10.126` | `172.16.10.127` | 64 | 62 |
| 3 | `172.16.10.128` | `172.16.10.129` | `172.16.10.190` | `172.16.10.191` | 64 | 62 |
| 4 | `172.16.10.192` | `172.16.10.193` | `172.16.10.254` | `172.16.10.255` | 64 | 62 |

### Step 6: Verify the subnet count and address ranges

The original `/24` network contains 256 addresses.

`4 subnets × 64 addresses per subnet = 256 addresses`

The ranges are consecutive and non-overlapping:

- Subnet 1 ends at `172.16.10.63`; Subnet 2 begins at `172.16.10.64`.
- Subnet 2 ends at `172.16.10.127`; Subnet 3 begins at `172.16.10.128`.
- Subnet 3 ends at `172.16.10.191`; Subnet 4 begins at `172.16.10.192`.
- Subnet 4 ends at `172.16.10.255`, the end of the original `/24` range.

All four subnets fit exactly inside `172.16.10.0/24`, with no overlap.


---

## Part 2: Packet Tracer Build Guide

### 1. Devices required

- One router with four usable, separately configurable Ethernet interfaces
- Four switches
- Eight PCs (two PCs per switch/subnet)
- Copper straight-through cables for PC-to-switch and switch-to-router links

Use a router/interface combination that exposes four routed Ethernet interfaces in Packet Tracer. The exact model and module availability can vary. If your router only has two or three usable interfaces, begin with the available subnets or choose a supported model/module that provides four routed interfaces. Do not assume a Layer 2 EtherSwitch module automatically provides four routed interfaces.

### 2. Build the topology

Create four separate LANs:

- Router interface 1 → Switch 1 → PC1 and PC2
- Router interface 2 → Switch 2 → PC3 and PC4
- Router interface 3 → Switch 3 → PC5 and PC6
- Router interface 4 → Switch 4 → PC7 and PC8

Use copper straight-through cables. Wait for the links to become active before testing.

### 3. Configure the router interfaces using the GUI

Open Router0, select the **Config** tab, and select each available Ethernet interface. For each interface, enter its IP address and subnet mask, then turn the interface **On** or enable it.

| Router interface | IP address | Subnet mask |
|---|---|---|
| Interface 1 (Subnet 1) | `172.16.10.1` | `255.255.255.192` |
| Interface 2 (Subnet 2) | `172.16.10.65` | `255.255.255.192` |
| Interface 3 (Subnet 3) | `172.16.10.129` | `255.255.255.192` |
| Interface 4 (Subnet 4) | `172.16.10.193` | `255.255.255.192` |

The exact interface names may be different on your router. Match each interface to the switch for its subnet. Each interface must be enabled. Because these are directly connected networks, the router learns their routes when the interfaces are configured and up; no static routes are needed for this topology.

### 4. Configure the PCs

For each PC, open **Desktop → IP Configuration**. Enter the IP address, subnet mask, and default gateway from the table below.

| PC | IP address | Subnet mask | Default gateway |
|---|---|---|---|
| PC1 (Subnet 1) | `172.16.10.2` | `255.255.255.192` | `172.16.10.1` |
| PC2 (Subnet 1) | `172.16.10.3` | `255.255.255.192` | `172.16.10.1` |
| PC3 (Subnet 2) | `172.16.10.66` | `255.255.255.192` | `172.16.10.65` |
| PC4 (Subnet 2) | `172.16.10.67` | `255.255.255.192` | `172.16.10.65` |
| PC5 (Subnet 3) | `172.16.10.130` | `255.255.255.192` | `172.16.10.129` |
| PC6 (Subnet 3) | `172.16.10.131` | `255.255.255.192` | `172.16.10.129` |
| PC7 (Subnet 4) | `172.16.10.194` | `255.255.255.192` | `172.16.10.193` |
| PC8 (Subnet 4) | `172.16.10.195` | `255.255.255.192` | `172.16.10.193` |

The router gateway is the first usable IP in each subnet. The two PCs in each LAN use unique addresses from that same subnet.

### 5. Test communication within each subnet

On a PC, open **Desktop → Command Prompt** and use `ping` to test the other PC on the same switch.

Examples:

- From PC1: `ping 172.16.10.3`
- From PC3: `ping 172.16.10.67`
- From PC5: `ping 172.16.10.131`
- From PC7: `ping 172.16.10.195`

A first ping may time out while ARP resolves MAC addresses. If that happens, try the ping again.

### 6. Test communication between different subnets

Try pings between PCs on different LANs. For example:

- From PC1: `ping 172.16.10.66` (PC3 in Subnet 2)
- From PC3: `ping 172.16.10.130` (PC5 in Subnet 3)
- From PC7: `ping 172.16.10.2` (PC1 in Subnet 1)

Successful pings confirm that the PCs, subnet masks, default gateways, router interfaces, and inter-subnet routing are configured correctly.

<img width="1100" height="511" alt="image" src="https://github.com/user-attachments/assets/413100a8-9763-4098-b02a-3ae16bdae02d" />
