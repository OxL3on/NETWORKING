# Lab 18: Observe ICMP Requests, Replies and Errors

## Objective
Understand how ICMP helps test network connectivity and reports network delivery errors.

## 1. What is ICMP?

ICMP (Internet Control Message Protocol) is a network-layer protocol used for diagnostics and reporting network errors.

The `ping` command uses ICMP Echo Request and Echo Reply messages to test connectivity.

## 2. ICMP Echo Request and Reply

When PC0 pings PC1:

1. PC0 sends an ICMP Echo Request to PC1.
2. PC1 receives the request and sends an ICMP Echo Reply.
3. PC0 receives the reply, indicating that ICMP communication succeeded.

**IPv4 ICMP types:**
- Echo Request: Type 8
- Echo Reply: Type 0

## 3. Common ICMP Error Messages

| ICMP Message | Purpose |
|---|---|
| Destination Unreachable | A destination or network cannot be reached, or delivery is not possible. |
| Time Exceeded | A packet's TTL expires before reaching its destination. |
| Redirect | Informs a host that a better next-hop route may be available. |
| Parameter Problem | Indicates an issue with a field in the IP header. |

## 4. Understanding TTL

TTL (Time To Live) limits how many router hops an IPv4 packet can make before being discarded.

Each router decreases the TTL value. When it reaches zero, the router discards the packet and may send an ICMP Time Exceeded message.

Traceroute uses this behavior to discover the routers along a path.

## 5. What Ping Results Mean

- **Reply received:** ICMP communication succeeded.
- **Request timed out:** No reply arrived before the timeout. The host may be unreachable, or ICMP replies may be filtered or lost.
- **Destination unreachable:** A device reports that the destination or delivery path cannot be reached.
- **Successful ping:** Confirms ICMP reachability at that moment, but does not guarantee that every application or service is working.

## 6. ICMP in Packet Tracer

In Simulation Mode, enable the ICMP filter and send a ping between two PCs.

Observe:
- The Echo Request travelling toward the destination.
- The Echo Reply returning to the sender.
- Any ICMP error messages generated when a supported failure occurs.

A failed ping does not always generate an ICMP error; some failures simply result in a timeout.

## Key Takeaway

ICMP supports network diagnostics. Echo Request and Reply messages test connectivity, while ICMP error messages help explain certain packet-delivery problems.
