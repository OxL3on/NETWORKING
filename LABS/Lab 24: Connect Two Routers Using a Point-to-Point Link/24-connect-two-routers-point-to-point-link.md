# Lab 24: Connect Two Routers Using a Point-to-Point Link

## Objective

Learn how to connect two routers directly so that two separate offices can communicate.

## Real-World Example

Imagine a company has two offices:

- **Office A:** Has its own LAN and Router A.
- **Office B:** Has its own LAN and Router B.

To connect both offices, we connect Router A and Router B using a point-to-point link.

```text
Office A                         Office B

   LAN A                            LAN B
     |                                |
  Router A -------- Link -------- Router B
```

## Topology

- 2 Cisco 2911 Routers
- 2 separate LANs (conceptual example)
- 1 Serial DCE cable between routers
- `HWIC-2T` module installed on both routers

## Point-to-Point Link Configuration

Network: `10.0.0.0/30`

Subnet Mask: `255.255.255.252`

| Device | Interface | IP Address |
|---|---|---|
| Router0 | Serial0/0/0 | 10.0.0.1 |
| Router1 | Serial0/0/0 | 10.0.0.2 |

## Router0 Configuration

```bash
enable
configure terminal
interface serial 0/0/0
ip address 10.0.0.1 255.255.255.252
clock rate 64000
no shutdown
```

## Router1 Configuration

```bash
enable
configure terminal
interface serial 0/0/0
ip address 10.0.0.2 255.255.255.252
no shutdown
```

**Note:** Apply `clock rate 64000` only on the DCE side.

## Verification

Check interface status:

```bash
show ip interface brief
```

Test connection from Router0:

```bash
ping 10.0.0.2
```

Expected result: Successful ping replies.

## Key Concepts

- **Point-to-Point Link:** Direct connection between two routers.
- **DCE:** Provides clock timing.
- **DTE:** Receives clock timing.
- **Clock Rate:** Controls serial link timing.
- **/30 Subnet:** Provides 2 usable IP addresses, one for each router.

## Important

Connecting two routers does not automatically allow their LANs to communicate. Routing configuration is needed for that.

## Result

Successfully connected two routers using a serial point-to-point link and verified communication using ping.
