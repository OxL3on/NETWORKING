# Calculate Network, Broadcast and Host Addresses

IP Address : 172.16.5.34/26
10101100.00010000.00000101.00100010

First 26 bits here represent the Network bits. (10101100.00010000.00000101.00)
So in order to determine the network address if we took the remainder of bits outside of the subnet mask and turn them into 0s that will be our network address. So 172.16.5.00000000 is the network address.

The broadcast address is the exact opposite of the network address. Taking everything after the 26th bit and turning it into 1s. So 172.16.5.00111111 (63)

Subtract 1 from the broadcast address and you'll get the last Host Address
And Add 1 with the network address and you'll get the first Host Address
Hosts : 172.16.5.00000001 - 172.16.5.00111110 (1-62)


Total usable hosts = 2^(host bits) - 2
