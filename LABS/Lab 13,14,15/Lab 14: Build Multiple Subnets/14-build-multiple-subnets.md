# Lab 14: Build Multiple Subnets

## Objective

Divide a larger IPv4 network into multiple equal-sized subnets, assign addresses to devices, and verify connectivity using Cisco Packet Tracer.

## 1. Network Requirements

Divide the network `192.168.20.0/24` into four equal-sized subnets.

Each subnet should support up to 30 usable host addresses.

## 2. Calculate the Subnet Prefix

A `/24` network contains 256 total addresses.

To create four equal-sized subnets:

`Number of borrowed bits = log2(4) = 2`

New prefix:

`/24 + 2 = /26`

Each `/26` subnet has:

- Total addresses: `2^6 = 64`
- Usable host addresses: `64 - 2 = 62`
- Subnet mask: `255.255.255.192`
- Block size: `256 - 192 = 64`

Each subnet therefore supports the required 30 hosts.

## 3. Calculate the Four Subnets

| Subnet | Network address | First host | Last host | Broadcast |
|---|---|---|---|---|
| 1 | `192.168.20.0/26` | `192.168.20.1` | `192.168.20.62` | `192.168.20.63` |
| 2 | `192.168.20.64/26` | `192.168.20.65` | `192.168.20.126` | `192.168.20.127` |
| 3 | `192.168.20.128/26` | `192.168.20.129` | `192.168.20.190` | `192.168.20.191` |
| 4 | `192.168.20.192/26` | `192.168.20.193` | `192.168.20.254` | `192.168.20.255` |

All four subnets are equal in size and do not overlap.

## 4. Build the Topology in Packet Tracer

Required devices:

- One router with four usable LAN interfaces, or a suitable supported interface module
- Four switches
- Two PCs per subnet

Connect each switch to a separate router interface. Connect two PCs to each switch using copper straight-through cables.

If your Packet Tracer router does not have enough Ethernet interfaces, use a compatible router/module or configure two subnets first and expand the topology when suitable interfaces are available.

## 5. Configure the Router Interfaces

Assign one gateway address to each subnet.

| Subnet | Router gateway |
|---|---|
| Subnet 1 | `192.168.20.1/26` |
| Subnet 2 | `192.168.20.65/26` |
| Subnet 3 | `192.168.20.129/26` |
| Subnet 4 | `192.168.20.193/26` |

Configure each router interface with its assigned IP address and subnet mask. Enable the interfaces if necessary.

## 6. Configure the PCs

Assign two unique IP addresses to the PCs in each subnet.

Example:

| Device | IP address | Mask | Default gateway |
|---|---|---|---|
| PC1 | `192.168.20.2` | `255.255.255.192` | `192.168.20.1` |
| PC2 | `192.168.20.3` | `255.255.255.192` | `192.168.20.1` |
| PC3 | `192.168.20.66` | `255.255.255.192` | `192.168.20.65` |
| PC4 | `192.168.20.67` | `255.255.255.192` | `192.168.20.65` |

Use the same pattern for the remaining subnets, ensuring each PC has a unique address in its assigned range.

## 7. Verify Connectivity

1. Check that connected links are active.
2. Ping between PCs within the same subnet.
3. Ping from a PC in one subnet to a PC in another subnet.
4. Confirm that the router forwards traffic between the subnets.
5. Use Packet Tracer Simulation Mode to observe ARP, ICMP, and router forwarding.

A successful same-subnet ping verifies local communication. A successful cross-subnet ping also verifies that the gateway and routing configuration work.

## 8. Verification Checklist

- [ ] Four equal-sized subnets calculated
- [ ] No overlapping address ranges
- [ ] Correct subnet mask on each device
- [ ] Correct router gateway for each subnet
- [ ] Successful same-subnet communication
- [ ] Successful communication between subnets
- [ ] Packet Tracer project saved

## Key Takeaway

Subnetting divides an address range into smaller networks. Devices communicate within their subnet using Layer 2 forwarding, while communication between different IP subnets requires a router or another Layer 3 forwarding device.
