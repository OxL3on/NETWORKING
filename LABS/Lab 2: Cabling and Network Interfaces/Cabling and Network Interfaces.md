Bro, for Lab 2: Cabling and Network Interfaces, here's everything you need to learn as a beginner. I'll keep it practical and focused on Cisco Packet Tracer, so you can understand the concepts and complete the lab using the GUI.

# Lab 2 — Cabling and Network Interfaces

Learning objectives

By the end of this lab, you should be able to:

- Identify network ports and interfaces on PCs, switches, and routers.
- Recognize common network cables.
- Choose the appropriate cable for a connection.
- Connect devices correctly in Packet Tracer.
- Understand link lights and troubleshoot connection problems.

# 1. What is a network interface?

A network interface is the connection through which a device sends and receives network traffic.

For example, your laptop might have two network interfaces:

- An Ethernet interface for a wired connection.
- A wireless interface for Wi-Fi.

[networking](https://images.openai.com/static-rsc-4/sHEXOiesmKKbrhYmnLr4e1AZMCoAd6ODtre-gWHNV0S9xX4yJjSYp8gUskpw3_q5-S_2Nw07Dc3RytOZ33WdQ7Bndu6U-JsuSSW0zDgmkh4tEit2_POKtHML4kniIZ9mijkHPeUKFh8NYgMr6vfofLHkGOD3xb5KdXCPNtQlR6BPgWJ_s0pFguV-h3CGkCnU?purpose=inline)

Ethernet interface

Connects to a wired network through an Ethernet cable.

[Upgrade & maintenance of your TUXEDO notebook - TUXEDO Computers](https://images.openai.com/static-rsc-4/zohHbI5FsjmN0JrDu7HcXzgA-dDxzUVPPhG6x_7Ni_ybwHJVyt99nMAkdigk43Sa1zulrPDPVRn_Esd3lpVdCa9E-_40BJ7BQiciGIu8TDZSUes5zEqt99K_7ltjGifkCTK9Iixz2TnZ9yWJlZsRHTHqK3oq5tCn7Ilv5VEdULI?purpose=inline)

Wireless interface

Connects to a Wi-Fi network using radio signals.

A network interface is often provided by a NIC (Network Interface Card). It might be built into the motherboard rather than being a separate card.

## Types of interfaces you'll see in Packet Tracer

FastEthernet

Commonly supports speeds up to 100 Mbps.

Example: `FastEthernet0` on a PC or `FastEthernet0/1` on a switch.

GigabitEthernet

Commonly supports speeds up to 1 Gbps.

Example: `GigabitEthernet0/0` on a router.

Serial interface

Found on certain router models and used for WAN connections in some Packet Tracer labs.

Console port

Used to access and configure a device locally. It is different from an Ethernet port and doesn't carry ordinary Ethernet network traffic.

Fiber/SFP interface

Used with compatible optical modules and fiber connections on supported equipment.

### How to read an interface name

For example, `GigabitEthernet0/1` tells you that you're looking at a Gigabit Ethernet interface.

On a switch, `FastEthernet0/1` usually means FastEthernet port 1 on that device. On a router, interface numbering depends on the device model.

You don't need to memorize every naming convention yet. Learn to identify the interface type and the port to which a cable should connect.

# 2. What is a network cable?

A network cable provides a physical path for signals to travel between devices.

Different cables are designed for different types of connections.

## The cables you should know

[MISUMI | Configurable Components | Distributor & Manufacturer - Buy Online](https://images.openai.com/static-rsc-4/zeARcNeyJnPfQGEiCaDSWhsgE_zCBxs6IbyUpQkN7G0B5qMifISsrnGnWfrpJTLFLomAl8EBN_Njj5kUs6R9EpQoA0sZ-CYa_eTJKM5wUAuhjQuTOAS1YeKULcWoDaSoEsppVCDOIK081F3Bhw0CzN9BCL25AlU2wRqCGfV4Dm0?purpose=inline)

1\. Copper straight-through Ethernet cable

Learn first

Used for common Ethernet connections, such as PC to switch and router to switch.

It is one of the main cables you'll use in your Packet Tracer labs.

[Crossover LAN Cable Pinout: When You Still Need One](https://images.openai.com/static-rsc-4/W_tQqOwYrTXv7sOV9voxTVe2BkOFDILQWk7q6WhLO-yC3gw2s64VfeMfcNQffM3eq9k2UllJBm7eM21uOywOLe8eYySYCjK2xme0W-7pZDsOq-o24-wQ1kechEt2ffS8CM_Zs3etA048mNj4PbxPPSsRgZbx1ZM4VWyfCyzSHKY?purpose=inline)

2\. Copper crossover cable

Traditionally used to connect similar Ethernet interfaces directly, such as switch to switch or PC to PC.

Modern equipment often supports Auto-MDI/MDIX, which can automatically accommodate either cable type. Packet Tracer may also handle some connections differently depending on the device.

[LANVIEW Fiber Optic Patch Cable - Lc-lc 9/125µm OS2 (Singlemode) Duplex Lszh - 2m Yellow - LVO231407 - Redcorp.com/en](https://images.openai.com/static-rsc-4/gdJbE5WtLwN2OdOiAz0iFN7ZJ0WVwNaGvUdKMRH7klr_0ZYcMXC5yTrpO2ar4EZ1xbZ1e7kb98rLIG8p3l2l0ETBpdl80cvBH-0a6snZ22VRr6fAexL1oK71cefowPp_kdmU_UWqnrqLljHkfzioT_artVotB5iFPSE69ASGVd0?purpose=inline)

3\. Fiber-optic cable

Carries data using light. Used for high-speed connections and longer-distance links.

Fiber requires compatible optical interfaces or transceivers at both ends.

[Bauxite - ESHAL INDUSTRIES](https://images.openai.com/static-rsc-4/sNqdWYAAsfiubsuN1-iy2Hka9PP6EaTEkvJdBXJm8-KYxtADyYsiC4HSPa9okarxSG21ba6f3VLgliTA2pVFL1pk6yCZnhGB2wkPYTr4NGTrt8N0iaHiB5wsRx1Bm4boGWvKe3uJnLPx_fM7pkmPW1HiUGm3xUg4TiGf9MRxVQw?purpose=inline)

4\. Serial cable

Used with supported router interfaces in some simulated WAN connections.

You may encounter DCE and DTE ends in Packet Tracer. The exact configuration depends on the lab and router model.

[CABLE USB A RJ45 1.8M PARA ROUTERS CISCO, AZUL](https://images.openai.com/static-rsc-4/TVCV0g6CTa3HrzcdjIgjFqPMu4rAg9Pm9om0FR8hcBsKoYC7o_oy7Iqh_xK6lDC_SiSIA057d8V4d7gIODo1qhMML5YqwkX684Iq6lplzjAsf7iLFyHEY4kDt3zgEj5ecEq5s0422kFwXCxac61q9xZdOcThMbjYR9hjNlEcpE8?purpose=inline)

5\. Console cable

Connects a computer's terminal interface to a network device's console port so you can configure it locally.

It is not a cable for ordinary Ethernet communication.

You may also encounter coaxial cables, which are used by cable internet systems and other technologies. You don't need to configure a coaxial internet connection for this basic Packet Tracer lab.

# 3. Which cable connects which devices?

This is the most important part of the lab.

| Connection                                  | Traditional cable choice                                   |
| ------------------------------------------- | ---------------------------------------------------------- |
| PC → Switch                                 | Straight-through                                           |
| Router → Switch                             | Straight-through                                           |
| Switch → Switch                             | Crossover                                                  |
| PC → PC directly                            | Crossover                                                  |
| Router → Router using Ethernet              | Crossover traditionally; depends on interface capabilities |
| PC → Router console port                    | Console cable                                              |
| Fiber-capable switch → Fiber-capable switch | Compatible fiber cable and interfaces                      |

Remember: these are traditional Ethernet cabling rules. Auto-MDI/MDIX allows many modern interfaces to work with either straight-through or crossover cables.

In Packet Tracer, you can use the Automatically Choose Connection Type lightning-bolt tool when you're unsure. However, for this lab, practise choosing the cables yourself so you understand the distinction.

# 4. What is an Ethernet port?

An Ethernet port is the physical socket into which you connect an Ethernet cable.

[Modem router switch with RJ45 ethernet plug ports](https://images.openai.com/static-rsc-4/N4U5K0elopqBnhzVT5Rw8aT3KWbAax7xm0kuR700YnByE_nVrdz1m5uRerg7nRiky8Y-URLMMQZQPrsN1nTWUC7LjjIM8HLtzZVT6yBHveL06WckPYr3HqmhHePw8ScBt_yDqgzg79uJpBPT7GXmb18fqGIkMaX8PceWbUlqy0W1hRDNpWEv29XQqwVwAYVC?purpose=inline)

For example, a switch might have these ports:

- `FastEthernet0/1`
- `FastEthernet0/2`
- `FastEthernet0/3`
- `GigabitEthernet0/1`

If you connect a PC to `FastEthernet0/1`, that tells you which switch port the PC is connected to.

This becomes useful later when you learn MAC address tables, VLANs, STP, and switch troubleshooting.

## Port vs. interface

People often use these words interchangeably in basic networking.

- Port: Often means the physical socket or connection point.
- Interface: The network interface through which communication occurs. It may refer to a physical interface or a logical interface, depending on the context.

For this lab, you can treat `FastEthernet0/1` as the particular physical network connection you select on a switch.

# 5. What is link status?

After connecting devices in Packet Tracer, look at the link indicators near the cables.

Green

Usually indicates that the link is operational.

Orange or amber

May indicate a transitional state, such as Spanning Tree Protocol (STP) processing, or another port state depending on the device.

Red

Typically indicates that the link is down or not operational.

The exact meaning depends on the device and Packet Tracer's current state. A green link doesn't automatically mean the entire network is configured correctly; IP settings and other configuration can still be wrong.

# 6. Speed, duplex and cable length

You don't need to master these topics today, but learn the basic definitions.

Speed is how fast an interface can transmit data. For example, 100 Mbps and 1 Gbps are different Ethernet speeds. The actual link rate depends on the capabilities and configuration of both ends.

Duplex describes whether an Ethernet connection can send and receive simultaneously.

- Half-duplex: sends or receives at a time.
- Full-duplex: can send and receive simultaneously.

Modern switched Ethernet links generally use full-duplex operation. Duplex mismatches can cause poor performance and errors.

Cable length: copper twisted-pair Ethernet commonly supports up to 100 metres per channel under the applicable cabling specifications. Fiber can support much longer distances, depending on the fiber type, transceivers, and link design.

You don't need to calculate cable lengths in this lab. Just understand that cables and interfaces have technical limits.

# 7. Your practical Packet Tracer lab

Now put the concepts into practice.

## Build this topology

PC0

FastEthernet0

Straight-through Ethernet cable

Switch0

FastEthernet0/1

Straight-through Ethernet cable

Router0

GigabitEthernet0/0

Interface names vary by Packet Tracer device model. Select interfaces actually available on your devices.

## Step-by-step

1. Open Cisco Packet Tracer and create a new project.
2. Add one PC, one switch, and one router.
3. Select the copper straight-through cable.
4. Click the PC and choose its Ethernet interface.
5. Click the switch and choose an available Ethernet port.
6. Repeat the process between the switch and router.
7. Observe the link indicators and wait for the initial connection process to settle.
8. Save your file as `02-cabling-and-interfaces.pkt`.

For this lab, you do not need to assign IP addresses or test a ping. Those belong to later labs.

## If a link doesn't come up

Check the following:

- Are you using a compatible cable and interface?
- Did you select the correct ports?
- Is the device powered on?
- Does that device require its interface to be enabled?
- Is the router interface administratively disabled by default?
- Is Packet Tracer still processing the connection or STP state?

If you see a red link between a router and switch, don't immediately assume the cable is wrong. Router interfaces may need to be enabled before the link becomes operational. Later, you'll learn how to configure this through the device's GUI or CLI.

# 8. Completion checklist

## Lab 2 progress

0/9

I can identify Ethernet ports on PCs, switches, and routers.

I understand the difference between FastEthernet and GigabitEthernet.

I can distinguish straight-through, crossover, fiber, serial, and console cables.

I know the traditional cable choices for PC-switch and router-switch connections.

I can select the correct device interfaces when connecting a cable.

I understand what green, amber, and red link indicators may mean.

I can identify some common reasons a link stays down.

I built the PC-switch-router topology in Packet Tracer.

I saved the completed .pkt file.

&#x20;Copy checklist

## What you don't need to learn yet

Don't spend time learning Ethernet pinout diagrams, detailed IEEE standards, SFP compatibility tables, fiber attenuation calculations, or serial clock-rate configuration right now. Those are useful in more specialized situations, but not necessary to complete this introductory lab.

Your next step: complete the small topology, recognize the interfaces and cables, and save your file. Then move to Lab 3, where you'll connect two PCs directly and start learning how addressing enables actual communication.
