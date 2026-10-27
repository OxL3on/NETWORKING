
# Lab 16: Identify Public, Private, Loopback and Link-Local Addresses


## 1. Public IPv4 address

Used for globally reachable internet communication, subject to routing and firewall rules.

Example: `8.8.8.8`

Public addresses are not one single private-style range. They must be distinguished from private and other special-purpose ranges.

## 2. Private IPv4 address

Used inside local networks, such as home, university or office networks. Internet access commonly uses NAT.

| Private range                 | CIDR             |
| ----------------------------- | ---------------- |
| `10.0.0.0–10.255.255.255`     | `10.0.0.0/8`     |
| `172.16.0.0–172.31.255.255`   | `172.16.0.0/12`  |
| `192.168.0.0–192.168.255.255` | `192.168.0.0/16` |

These are the three private ranges defined by RFC 1918.


## 3. Loopback address

Used by a device to communicate with itself. Traffic stays inside the device rather than travelling across the physical network.

Range: `127.0.0.0/8`

Common example: `127.0.0.1`


## 4. Link-local address

Used for communication between devices on the same local network link. IPv4 link-local addresses can be automatically assigned when normal configuration, such as DHCP, is unavailable.

Range: `169.254.0.0/16`

Example: `169.254.20.15`

These addresses are not forwarded by routers.
