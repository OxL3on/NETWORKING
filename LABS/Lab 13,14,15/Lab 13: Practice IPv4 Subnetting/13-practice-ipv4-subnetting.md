# Lab 13: Practice IPv4 Subnetting

## Worked Example: Calculate Network, Broadcast and Host Addresses

**Given IP Address:** `172.22.91.50/20`

### Step 1: Calculate the Subnet Mask

The `/20` prefix means the first 20 bits represent the network portion.

Subnet mask: `255.255.240.0`

### Step 2: Calculate the Block Size

The third octet is the interesting octet because its subnet-mask value is `240`.

Block Size = `256 - 240 = 16`

The third-octet ranges increase in increments of 16:

`0–15, 16–31, 32–47, 48–63, 64–79, 80–95, 96–111, ...`

The given IP has `91` in its third octet, so it belongs to the `80–95` range.

### Step 3: Calculate the Network Address (NA)

Use the first value of the matching block and set the remaining host bits to zero.

**Network Address:** `172.22.80.0`

### Step 4: Calculate the Broadcast Address (BA)

Use the last value of the matching block and set all host bits to one.

**Broadcast Address:** `172.22.95.255`

### Step 5: Calculate the First Usable Host (FHA)

Add `1` to the network address.

`172.22.80.0 + 1 = 172.22.80.1`

**First Usable Host:** `172.22.80.1`

### Step 6: Calculate the Last Usable Host (LHA)

Subtract `1` from the broadcast address.

`172.22.95.255 - 1 = 172.22.95.254`

**Last Usable Host:** `172.22.95.254`

### Step 7: Calculate Total and Usable Addresses

IPv4 addresses contain 32 bits.

Host Bits = `32 - 20 = 12`

Total Addresses = `2^12 = 4,096`

Usable Host Addresses = `4,096 - 2 = 4,094`

The two excluded addresses are the network address and broadcast address.

## Final Results

| Property | Result |
|---|---|
| IP Address | `172.22.91.50/20` |
| Subnet Mask | `255.255.240.0` |
| Block Size | 16 |
| Network Address | `172.22.80.0` |
| Broadcast Address | `172.22.95.255` |
| First Usable Host | `172.22.80.1` |
| Last Usable Host | `172.22.95.254` |
| Total Addresses | 4,096 |
| Usable Host Addresses | 4,094 |

## General Procedure

1. Convert the CIDR prefix into a subnet mask.
2. Identify the interesting octet.
3. Calculate the block size using `256 - subnet-mask value`.
4. Find the block containing the given IP address.
5. Use the first address in the block as the network address.
6. Use the last address in the block as the broadcast address.
7. Add one to the network address and subtract one from the broadcast address to find the usable host range.
8. Calculate total addresses using `2^(32 - prefix)` and conventional usable hosts by subtracting two.

**Key Takeaway:** The block size identifies the correct subnet range. Once the range is known, the network, broadcast, first host, last host, and usable host count can be calculated systematically.
