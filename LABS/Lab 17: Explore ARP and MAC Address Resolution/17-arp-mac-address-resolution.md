
# Lab 17: Explore ARP and MAC Address Resolution

## Step 1 — Understand ARP

ARP (Address Resolution Protocol) finds the MAC address associated with an IPv4 address on a local network. For example, PC0 wants to send data to PC1. PC0 knows PC1's IP address, but it needs PC1's MAC address to send an Ethernet frame.

<img width="658" height="176" alt="image" src="https://github.com/user-attachments/assets/7d512ca8-9ae6-47b3-bfc0-43d8017d71a3" />

ARP works in this sequence:

1. ARP Request: PC0 broadcasts a message asking which device has `192.168.1.20`.
2. ARP Reply: PC1 responds with its MAC address.
3. ARP Cache: PC0 stores the IP-to-MAC mapping temporarily.
4. Ethernet Frame: PC0 sends the data using PC1's MAC address as the destination MAC.

Remember the difference:

- ARP: Maps an IPv4 address to a MAC address.
- Switch MAC address table: Maps learned MAC addresses to switch ports.

## Step 2 — Build the topology in Packet Tracer

Use three devices:

- One switch (2960)
- PC0
- PC1

Connect both PCs to the switch using Copper Straight-Through cables.

## Step 3 — Configure the PCs

Open each PC and select Desktop → IP Configuration → Static.

| Setting         | PC0             | PC1             |
| --------------- | --------------- | --------------- |
| IPv4 address    | `192.168.1.10`  | `192.168.1.20`  |
| Subnet mask     | `255.255.255.0` | `255.255.255.0` |
| Default gateway | Leave blank     | Leave blank     |

Wait for both links to become green.

## Step 4 — Observe ARP in Simulation Mode

1. Switch Packet Tracer from Realtime to Simulation mode.
2. Open Edit Filters and select ARP and ICMP. Clear the existing event list if necessary.
3. Open PC0 → Desktop → Command Prompt.
4. Run `ping 192.168.1.20`.
5. Use Capture/Forward to inspect each event and observe the ARP request, ARP reply, and ICMP packets.

The first ping may take longer because ARP resolution occurs before the ICMP exchange. If the ARP entry is already cached, clear the simulation or restart the test so you can observe the initial request.

## Step 5 — Understand what happens

| Event | What happens                                                             |
| ----- | ------------------------------------------------------------------------ |
| 1     | PC0 checks its ARP cache for PC1's MAC address.                          |
| 2     | If no entry exists, PC0 broadcasts an ARP Request.                       |
| 3     | Switch0 floods the broadcast to other ports in the same VLAN.            |
| 4     | PC1 recognizes its IP and sends an ARP Reply containing its MAC address. |
| 5     | PC0 stores the mapping in its ARP cache.                                 |
| 6     | PC0 sends an ICMP Echo Request using PC1's destination MAC address.      |
| 7     | PC1 sends an ICMP Echo Reply, and the ping succeeds.                     |

## Step 6 — Verify the ARP cache

After the ping, open PC0's Command Prompt and try:

```
arp -a
```


