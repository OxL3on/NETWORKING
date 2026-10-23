# Lab 13: Practice IPv4 Subnetting

## Objective

Practice calculating subnet masks, network addresses, broadcast addresses, usable host ranges, block sizes, and subnet capacities from IPv4 addresses and CIDR prefixes.

## 1. Understand CIDR and Subnet Masks

An IPv4 address contains 32 bits divided into four octets. A CIDR prefix indicates how many bits belong to the network portion.

Example:

- IP address: `192.168.10.77/26`
- Network bits: 26
- Host bits: `32 - 26 = 6`
- Subnet mask: `255.255.255.192`

## 2. Calculate Total and Usable Addresses

Formulas:

- Host bits = `32 - prefix`
- Total addresses = `2^host bits`
- Conventional usable hosts = `2^host bits - 2`

For a `/26` subnet:

- Host bits: `32 - 26 = 6`
- Total addresses: `2^6 = 64`
- Usable host addresses: `64 - 2 = 62`

The network and broadcast addresses are excluded from the conventional usable-host count.

## 3. Find the Block Size

Identify the subnet-mask octet that is neither `255` nor `0`.

Formula:

`Block size = 256 - relevant subnet-mask octet`

For `/26`, the subnet mask is `255.255.255.192`.

`256 - 192 = 64`

The subnet boundaries in the last octet are:

`0, 64, 128, 192`

## 4. Calculate Network and Host Addresses

Given:

`192.168.10.77/26`

The address `77` belongs to the block `64–127`.

Therefore:

| Property | Result |
|---|---|
| IP address | `192.168.10.77/26` |
| Subnet mask | `255.255.255.192` |
| Network address | `192.168.10.64` |
| Broadcast address | `192.168.10.127` |
| First usable host | `192.168.10.65` |
| Last usable host | `192.168.10.126` |
| Total addresses | 64 |
| Usable host addresses | 62 |

Procedure:

1. Convert the CIDR prefix into a subnet mask.
2. Calculate the block size in the relevant octet.
3. Identify the block containing the given IP address.
4. Use the block's first address as the network address.
5. Use the block's last address as the broadcast address.
6. Add one to the network address for the first host.
7. Subtract one from the broadcast address for the last host.
8. Calculate the usable host count.

For prefixes such as `/13` and `/20`, the relevant octet may be the second or third octet instead of the fourth.

## 5. Calculate a Subnet from Host Requirements

Example: A network needs 50 usable host addresses.

- 5 host bits provide `2^5 - 2 = 30` hosts.
- 6 host bits provide `2^6 - 2 = 62` hosts.

Therefore:

`Prefix = 32 - 6 = /26`

A `/26` is the smallest conventional IPv4 subnet that supports 50 hosts.

## 6. Practice Tasks

For each supplied IPv4 address and prefix, calculate:

- Subnet mask
- Network address
- Broadcast address
- First usable host
- Last usable host
- Total addresses
- Usable host addresses

Also practise selecting the smallest subnet for a required number of hosts and calculating subnet boundaries in the second and third octets.

## 7. Verification Checklist

- [ ] Correct subnet mask for the CIDR prefix
- [ ] Correct block size
- [ ] Correct network and broadcast addresses
- [ ] Correct first and last usable hosts
- [ ] Correct usable host count
- [ ] Correct calculations for different CIDR prefixes

## Key Takeaway

IPv4 subnetting becomes manageable when the subnet mask, block size, address range, and host count are calculated systematically rather than guessed or memorized.
