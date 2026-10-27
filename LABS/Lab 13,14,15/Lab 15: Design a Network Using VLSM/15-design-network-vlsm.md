# Lab 15: Design a Network Using VLSM

## Objective
Allocate different-sized subnets based on each department's host requirements using VLSM (Variable Length Subnet Masking).

## Problem

Available Network: `172.16.0.0/23`

| Department | Hosts Required |
|---|---:|
| Engineering | 180 |
| Operations | 90 |
| IT | 45 |
| Management | 20 |

## Step 1: Check the Original Network

A `/23` network contains:

- Total addresses: `2^(32-23) = 512`
- Address range: `172.16.0.0 – 172.16.1.255`

Allocate the largest subnet first to avoid wasting address space.

## Step 2: Calculate Each Subnet

### 1. Engineering — 180 Hosts

- 7 host bits provide 126 usable hosts (not enough).
- 8 host bits provide 254 usable hosts.
- Prefix: `32 - 8 = /24`
- Subnet mask: `255.255.255.0`

Allocate: `172.16.0.0/24`

- Network: `172.16.0.0`
- First host: `172.16.0.1`
- Last host: `172.16.0.254`
- Broadcast: `172.16.0.255`

Next available address: `172.16.1.0`

### 2. Operations — 90 Hosts

- 7 host bits provide `2^7 - 2 = 126` usable hosts.
- Prefix: `32 - 7 = /25`
- Subnet mask: `255.255.255.128`
- Block size: `256 - 128 = 128`

Allocate: `172.16.1.0/25`

- Network: `172.16.1.0`
- First host: `172.16.1.1`
- Last host: `172.16.1.126`
- Broadcast: `172.16.1.127`

Next available address: `172.16.1.128`

### 3. IT — 45 Hosts

- 6 host bits provide `2^6 - 2 = 62` usable hosts.
- Prefix: `32 - 6 = /26`
- Subnet mask: `255.255.255.192`
- Block size: `256 - 192 = 64`

Allocate: `172.16.1.128/26`

- Network: `172.16.1.128`
- First host: `172.16.1.129`
- Last host: `172.16.1.190`
- Broadcast: `172.16.1.191`

Next available address: `172.16.1.192`

### 4. Management — 20 Hosts

- 5 host bits provide `2^5 - 2 = 30` usable hosts.
- Prefix: `32 - 5 = /27`
- Subnet mask: `255.255.255.224`
- Block size: `256 - 224 = 32`

Allocate: `172.16.1.192/27`

- Network: `172.16.1.192`
- First host: `172.16.1.193`
- Last host: `172.16.1.222`
- Broadcast: `172.16.1.223`

## Step 3: Final VLSM Table

| Department | Network / Prefix | Usable Host Range | Broadcast |
|---|---|---|---|
| Engineering | `172.16.0.0/24` | `172.16.0.1–254` | `172.16.0.255` |
| Operations | `172.16.1.0/25` | `172.16.1.1–126` | `172.16.1.127` |
| IT | `172.16.1.128/26` | `172.16.1.129–190` | `172.16.1.191` |
| Management | `172.16.1.192/27` | `172.16.1.193–222` | `172.16.1.223` |

## Step 4: Verify Address Space

Total allocated addresses:

`256 + 128 + 64 + 32 = 480`

Original network: `512` addresses.

Remaining: `512 - 480 = 32` addresses.

Unused block: `172.16.1.224/27`

All subnets fit inside the original `/23` without overlapping.

## Key Takeaway

1. Sort host requirements from largest to smallest.
2. Find the smallest prefix that supports each requirement.
3. Allocate each subnet at the next valid network boundary.
4. Calculate network, broadcast, and usable host ranges.
5. Verify that all subnets fit inside the original network without overlap.
