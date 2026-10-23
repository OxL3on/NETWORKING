# Lab 15: Design a Network Using VLSM

## Objective

Design a network using Variable Length Subnet Masking (VLSM), allocating different-sized subnets based on host requirements while avoiding overlapping address ranges.

## 1. Network Requirements

The organization has the address block:

`192.168.50.0/24`

It needs four subnets:

| Department | Required hosts |
|---|---:|
| Department A | 100 |
| Department B | 50 |
| Department C | 20 |
| Department D | 10 |

## 2. Sort the Requirements

Always start with the largest host requirement.

Order:

1. Department A — 100 hosts
2. Department B — 50 hosts
3. Department C — 20 hosts
4. Department D — 10 hosts

This helps prevent smaller subnet allocations from consuming address space needed by a larger subnet.

## 3. Calculate the Required Prefix for Each Department

Select the smallest conventional subnet that provides enough usable hosts.

### Department A: 100 hosts

- 7 host bits provide `2^7 - 2 = 126` usable hosts.
- Prefix: `32 - 7 = /25`.
- Subnet mask: `255.255.255.128`.

Allocate `192.168.50.0/25`.

### Department B: 50 hosts

- 6 host bits provide `2^6 - 2 = 62` usable hosts.
- Prefix: `/26`.
- Subnet mask: `255.255.255.192`.

The next available boundary after the `/25` subnet is `192.168.50.128`.

Allocate `192.168.50.128/26`.

### Department C: 20 hosts

- 5 host bits provide `2^5 - 2 = 30` usable hosts.
- Prefix: `/27`.
- Subnet mask: `255.255.255.224`.

The next available boundary is `192.168.50.192`.

Allocate `192.168.50.192/27`.

### Department D: 10 hosts

- 4 host bits provide `2^4 - 2 = 14` usable hosts.
- Prefix: `/28`.
- Subnet mask: `255.255.255.240`.

The next available boundary is `192.168.50.224`.

Allocate `192.168.50.224/28`.

## 4. Final VLSM Allocation Table

| Department | Prefix | Network address | Usable host range | Broadcast |
|---|---|---|---|---|
| A | `/25` | `192.168.50.0` | `192.168.50.1–126` | `192.168.50.127` |
| B | `/26` | `192.168.50.128` | `192.168.50.129–190` | `192.168.50.191` |
| C | `/27` | `192.168.50.192` | `192.168.50.193–222` | `192.168.50.223` |
| D | `/28` | `192.168.50.224` | `192.168.50.225–238` | `192.168.50.239` |

These allocations fit inside `192.168.50.0/24` and do not overlap.

Remaining addresses: `192.168.50.240–192.168.50.255`, a total of 16 addresses that can be reserved or allocated later if requirements permit.

## 5. Build the Network in Packet Tracer

Required devices:

- One router with enough interfaces for the proposed subnets, or an appropriate supported design
- One switch per department
- At least two PCs per department

Connect the switches to their corresponding router interfaces. Configure the router gateway address for each subnet using the first usable address.

Example:

| Department | Gateway |
|---|---|
| A | `192.168.50.1/25` |
| B | `192.168.50.129/26` |
| C | `192.168.50.193/27` |
| D | `192.168.50.225/28` |

Assign unique host addresses, correct subnet masks, and the appropriate default gateway to each PC.

## 6. Verify the Design

1. Confirm that every PC has an address within its allocated subnet.
2. Confirm that no network or broadcast address is assigned to a PC.
3. Verify local communication within each department.
4. Verify communication between departments through the router.
5. Use Simulation Mode to inspect ARP, ICMP, and packet forwarding.

## 7. Verification Checklist

- [ ] Host requirements sorted from largest to smallest
- [ ] Smallest suitable prefix selected for each department
- [ ] Correct network and broadcast addresses calculated
- [ ] No overlapping subnet allocations
- [ ] Every subnet fits inside the original `/24`
- [ ] Correct gateway and mask assigned to each device
- [ ] Communication verified within and between departments
- [ ] Packet Tracer project saved

## Key Takeaway

VLSM conserves IPv4 address space by assigning subnet sizes according to actual host requirements. Allocate the largest subnet first, calculate each network boundary carefully, and verify that all address ranges remain non-overlapping.
