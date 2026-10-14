# Lab 2: Network Interfaces and Cabling

## 1. What Are Network Interfaces and Ports?

A **network interface** allows a device to send and receive data over a network.

For example:
- A PC uses an Ethernet interface for a wired connection.
- A laptop may use an Ethernet interface and a wireless interface.
- A switch has many interfaces to connect PCs, servers, and other network devices.

A physical network interface is often called a **port**. In basic networking, these terms are frequently used interchangeably.

### RJ-45 Ports and Connectors

An RJ-45 port is the familiar Ethernet socket found on many PCs, routers, and switches.

An RJ-45 connector is the plug at the end of a copper Ethernet cable that fits into the port.

These connectors follow industry standards, allowing compatible devices and cables from different manufacturers to work together.

### Ethernet

**Ethernet** is a family of networking standards and technologies used primarily for wired local area networks (LANs).

It defines how devices communicate over Ethernet links, including aspects of cabling, signaling, and data transmission.

IEEE 802.3 is the main family of standards for Ethernet.

Network standards matter because devices need to follow compatible rules to communicate properly.

---

## 2. Network Speed: Bits and Bytes

Network speed is commonly measured in **bits per second (bps)**.

A bit is a binary value: `0` or `1`.

A byte contains 8 bits.

### Common Units

| Unit | Value |
|---|---:|
| 1 bit | One binary digit |
| 1 byte | 8 bits |
| 1 Kbps | 1,000 bits per second |
| 1 Mbps | 1,000,000 bits per second |
| 1 Gbps | 1,000,000,000 bits per second |
| 1 Tbps | 1,000,000,000,000 bits per second |

Network speeds generally use decimal units, where each larger unit is 1,000 times the previous one.

### Bits vs. Bytes

Network speeds use bits, while file sizes are commonly displayed in bytes.

For example:
- `100 Mbps` means 100 million bits per second.
- `100 MB` means 100 megabytes of data.
- 100 Mbps is theoretically equivalent to 12.5 MB/s before protocol overhead and other limitations.

**Remember:** A byte contains 8 bits, so bits per second and bytes per second are not the same thing.

---

## 3. Ethernet Standards and Speeds

Ethernet standards specify supported speeds, cabling requirements, and other technical characteristics.

### Common Copper Ethernet Standards

| Standard | Common name | Speed | Typical maximum copper channel length |
|---|---|---:|---:|
| 10BASE-T | Ethernet | 10 Mbps | 100 metres |
| 100BASE-TX | Fast Ethernet | 100 Mbps | 100 metres |
| 1000BASE-T | Gigabit Ethernet | 1 Gbps | 100 metres |
| 10GBASE-T | 10 Gigabit Ethernet | 10 Gbps | 100 metres |

These are common examples using twisted-pair copper cabling.

### Understanding the Names

- **10, 100, 1000, 10G:** indicate the nominal data rate.
- **BASE:** refers to baseband signaling.
- **T:** indicates twisted-pair copper cabling in these standard names.

For example, `1000BASE-T` means Gigabit Ethernet over twisted-pair copper cable.

A cable and both connected interfaces must support compatible Ethernet standards to achieve the intended link speed.

---

## 4. UTP Ethernet Cables

**UTP stands for Unshielded Twisted Pair.**

UTP cables are widely used to connect PCs, switches, routers, and other Ethernet devices.

A typical UTP Ethernet cable contains:
- Four pairs of twisted copper wires.
- Eight individual wires in total.
- An RJ-45 connector at each end.

### Why Are the Wires Twisted?

The wires are twisted together in pairs to help reduce electromagnetic interference (EMI).

Because UTP has no additional metallic shield around the pairs, it can still be affected by electrical interference.

### How Many Wires Are Used?

For common Ethernet standards:

- **10BASE-T and 100BASE-TX:** use two pairs, or four wires.
- **1000BASE-T and 10GBASE-T:** use all four pairs, or eight wires.

Gigabit Ethernet and 10 Gigabit Ethernet over twisted-pair copper use all four pairs for bidirectional communication.

### Advantages of UTP

- Generally inexpensive.
- Easy to install.
- Commonly available.
- Suitable for connecting end devices to access switches.
- Supports common LAN speeds over distances up to 100 metres per channel when correctly installed.

### Limitations of UTP

- Twisted-pair copper Ethernet channels are generally limited to 100 metres.
- Copper can be affected by electromagnetic interference.
- Copper cabling can require more care around electrical noise than fiber-optic cabling.

---

## 5. Straight-Through Ethernet Cable

A **straight-through cable** connects the corresponding pins at both ends.

For example:
- Pin 1 connects to pin 1.
- Pin 2 connects to pin 2.
- Pin 3 connects to pin 3.

### Common Traditional Uses

- PC → Switch
- Router → Switch
- Server → Switch
- Firewall → Switch

These devices traditionally use complementary transmit and receive pairs when connected in these combinations.

### Basic Idea

A straight-through cable does not cross or swap the wiring pairs between its two ends.

---

## 6. Crossover Ethernet Cable

A **crossover cable** swaps the relevant transmit and receive pairs between its ends.

For traditional 10BASE-T and 100BASE-TX wiring, the important pins are:

- Pins 1 and 2.
- Pins 3 and 6.

A traditional crossover cable connects:
- Pin 1 on one end to pin 3 on the other end.
- Pin 2 on one end to pin 6 on the other end.
- Pin 3 on one end to pin 1 on the other end.
- Pin 6 on one end to pin 2 on the other end.

### Common Traditional Uses

- PC → PC directly.
- Switch → Switch.
- Router → Router over Ethernet.
- PC → Router over Ethernet.

These examples assume compatible Ethernet interfaces that do not automatically adapt their transmit and receive wiring.

### Straight-Through vs. Crossover

| Feature | Straight-through | Crossover |
|---|---|---|
| Wiring | Corresponding pins connect straight through | Transmit and receive pairs are crossed |
| Traditional use | PC-to-switch, router-to-switch | PC-to-PC, switch-to-switch |
| Main purpose | Connect complementary interface types | Connect similar interface types that need crossed pairs |

### Important: Auto-MDI/MDIX

Many modern Ethernet interfaces support **Auto-MDI/MDIX**.

This feature automatically detects and adapts to the wiring arrangement, allowing compatible devices to work with either a straight-through or crossover cable.

Therefore, you usually do not need to worry about cable crossover rules when working with modern equipment.

However, you should understand the traditional rules because they explain why certain older connections require specific cables.

---

## 7. Transmit and Receive Pins

The lesson explains the traditional transmit/receive wiring used by 10BASE-T and 100BASE-TX Ethernet interfaces.

- **Tx:** Transmit; sends data.
- **Rx:** Receive; receives data.

For traditional PC, router, and firewall interfaces:
- Pins 1 and 2 transmit data.
- Pins 3 and 6 receive data.

For a traditional switch interface:
- Pins 1 and 2 receive data.
- Pins 3 and 6 transmit data.

This difference explains why straight-through cables traditionally work between a PC and a switch, while crossover cables are used between similar interfaces.

Modern Auto-MDI/MDIX can adapt to these differences automatically.

You do not need to memorize every pin immediately, but understand how the transmit and receive pairs work.

---

## 8. Gigabit Ethernet and Higher Speeds

1000BASE-T and 10GBASE-T use all four twisted pairs in the Ethernet cable.

Unlike traditional 10BASE-T and 100BASE-TX, where transmit and receive functions use separate pairs, higher-speed twisted-pair Ethernet uses bidirectional signaling on the pairs.

This means each pair participates in sending and receiving data.

Using all four pairs helps support the higher data rates.

**Key point:** Gigabit Ethernet is not simply Fast Ethernet operating faster. It uses different signaling techniques and all four pairs of the cable.

---

## 9. Fiber-Optic Cabling

Fiber-optic cable carries data using pulses of light through glass or plastic fibers rather than electrical signals through copper wires.

Fiber is commonly used for:
- High-speed network connections.
- Connections between switches.
- Links between buildings.
- Long-distance network connections.

### Advantages of Fiber

- Supports longer distances than ordinary twisted-pair copper Ethernet.
- Supports high data rates.
- Is resistant to electromagnetic interference.
- Does not emit the same electrical signals outside the cable as copper wiring.

Fiber can still be physically damaged and must be handled and installed correctly.

### Limitations of Fiber

- Equipment and transceivers can cost more.
- Fiber and connectors require appropriate handling and cleaning.
- Both ends need compatible optical interfaces and transceivers.

---

## 10. Structure of a Fiber-Optic Cable

A fiber-optic cable contains several layers.

1. **Core:** The central part through which light travels.
2. **Cladding:** Surrounds the core and helps keep light confined within it.
3. **Buffer or protective coating:** Protects the fiber.
4. **Outer jacket:** Provides additional physical protection.

The core and cladding are essential for guiding light through the fiber.

### Transmit and Receive

Many duplex fiber Ethernet connections use two separate fibers:
- One carries transmitted data.
- The other carries received data.

The transmitting end of one fiber connects to the receiving end at the opposite device, and vice versa.

Some fiber systems use different arrangements, so this describes a common duplex connection.

---

## 11. Single-Mode Fiber vs. Multimode Fiber

There are two major types of optical fiber.

### Multimode Fiber (MMF)

Multimode fiber has a wider core that allows multiple modes of light to propagate.

Characteristics:
- Commonly used for shorter-distance links.
- Often less expensive to use for suitable short-range applications.
- Common in buildings and data centers.
- Supported distances depend on the fiber grade, data rate, and transceiver.

### Single-Mode Fiber (SMF)

Single-mode fiber has a much narrower core and supports one propagation mode.

Characteristics:
- Commonly used for longer-distance links.
- Supports much longer distances than typical multimode applications.
- Often uses laser-based optical transmitters.
- Equipment cost depends on the transceiver and application.

### Comparison

| Feature | Multimode | Single-mode |
|---|---|---|
| Core | Wider | Narrower |
| Typical applications | Shorter links | Longer links |
| Distance capability | Shorter than comparable single-mode links | Can support much longer links |
| Equipment costs | Often economical for short-range links | Depends on the optic and link requirements |

**Remember:** choose fiber based on the supported distance, data rate, optical equipment, and installation requirements—not just because one type is always cheaper.

---

## 12. SFP Transceivers

**SFP stands for Small Form-factor Pluggable.**

An SFP transceiver is a removable module that fits into a compatible port on a network device.

It allows a switch or router to support an appropriate type of network connection.

Depending on the module, it may support:
- Fiber-optic connections.
- Copper Ethernet connections.
- Different speeds and distances.

The device, module, fiber type, connectors, and link specifications must be compatible.

For example, a compatible fiber SFP module can allow two switches to communicate over fiber-optic cable.

### SFP and Fiber

A common fiber connection consists of:
- A compatible optical transceiver at each end.
- A suitable fiber cable.
- Transmit-to-receive connections between the two devices.

Do not assume that every SFP module supports every fiber type or speed.

---

## 13. Common Fiber Ethernet Standards

The lesson introduces several examples of fiber Ethernet standards.

| Standard | Speed | Typical fiber type | Example maximum distance from the lesson |
|---|---:|---|---:|
| 1000BASE-LX | 1 Gbps | Single-mode or supported multimode | Up to 5 km on single-mode; up to 550 m on multimode in the example |
| 10GBASE-SR | 10 Gbps | Multimode | Up to 400 m with suitable supported fiber |
| 10GBASE-LR | 10 Gbps | Single-mode | Up to 10 km |
| 10GBASE-ER | 10 Gbps | Single-mode | Up to 30 km |

These distances are examples, not universal guarantees. Actual supported distances depend on the Ethernet specification, fiber type and grade, optical transceivers, and link design.

You do not need to memorize every fiber standard for your first Packet Tracer lab. Focus on understanding why different types of fiber exist and how they are selected.

---

## 14. Copper UTP vs. Fiber-Optic Cable

| Feature | Copper UTP | Fiber-optic |
|---|---|---|
| Signal | Electrical | Light |
| Typical connector | RJ-45 | Depends on the fiber system |
| Common use | PCs to access switches | Switch uplinks and longer links |
| Typical maximum distance | 100 m per standard Ethernet channel | Depends on the optic and fiber type; can be much longer |
| Interference | Can be affected by EMI | Resistant to EMI |
| Cost | Often inexpensive for short links | Equipment and installation costs vary |
| Security considerations | Can be vulnerable to physical tapping | Can also be tapped, though practical access and methods differ |

Both technologies are important in modern networks. Copper is common for end devices, while fiber is common for high-speed uplinks and longer-distance connections.

---

## 15. Quick Revision: Which Cable Should You Choose?

| Connection | Traditional choice |
|---|---|
| PC → Switch | Straight-through |
| Router → Switch | Straight-through |
| Switch → Switch | Crossover |
| PC → PC directly | Crossover |
| Router → Router over Ethernet | Crossover |
| PC → Router console port | Console cable |
| Switch → Switch over fiber | Compatible fiber transceivers and fiber cable |

These are traditional examples. Auto-MDI/MDIX can remove the need for crossover cables on supported Ethernet interfaces.

For Packet Tracer, the automatic connection tool is useful when you are unsure, but practise manual selection to learn the differences.

