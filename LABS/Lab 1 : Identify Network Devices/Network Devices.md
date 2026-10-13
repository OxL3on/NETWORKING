## 1. Modem

A **modem** connects a network to an Internet Service Provider (ISP) through a supported internet connection.

Modem stands for **Modulator-Demodulator**. Traditional modems convert signals between forms suitable for the communication medium and digital data. The exact technology depends on the internet connection.

### Types of Modems

- **Cable Modem:** Uses coaxial cable.
- **DSL Modem:** Uses telephone lines.
- **Fiber ONT:** Terminates a fiber-optic internet connection.
- **Cellular Modem:** Connects through mobile networks such as 4G or 5G.
- **Satellite Modem:** Communicates through a satellite internet connection.

**Key point:** The modem or ONT provides the connection to the ISP. Some internet services use different equipment or combine several functions into one device.

## 2. Router

A **router** connects different IP networks and forwards packets between them.

For example, a home router connects the local network to the internet. It examines the destination IP address and uses its routing table to decide where to forward each packet.

### Main Functions

- Routes packets between different networks.
- Uses a `routing table` to select a route.
- Often acts as the default gateway for devices on a local network.
- Commonly provides DHCP to assign IP addresses.
- Often performs NAT/PAT so multiple private devices can share a public IPv4 address.
- Many home routers also include a switch, wireless access point, and firewall.

**Example:** A PC on `192.168.1.0/24` wants to communicate with a server on a different subnet. It sends the packet to its default gateway, which routes it toward the destination.

**Key point:** A switch connects devices within a LAN; a router connects IP networks.

## 3. Switch

A **network switch** connects multiple wired devices within a Local Area Network (LAN).

Most traditional Ethernet switches operate at **Layer 2 (Data Link Layer)** of the OSI model.

### How It Works

A switch learns source MAC addresses from incoming Ethernet frames and records which MAC addresses are reachable through which ports.

When a frame arrives, the switch examines its destination MAC address and forwards it through the appropriate port when the destination is known. Unknown unicast frames and broadcast frames are generally flooded within the relevant VLAN.

### Main Functions

- Connects PCs, printers, servers, and other wired devices.
- Learns and maintains a MAC address table.
- Forwards Ethernet frames between devices.
- Supports VLANs on managed switches.
- Helps reduce unnecessary traffic compared with a hub.

**Key point:** A switch primarily forwards Ethernet frames using MAC addresses, while a router forwards IP packets between networks.

## 4. Wireless Access Point (WAP)

A **wireless access point (AP)** allows wireless devices to connect to a network using Wi-Fi.

It commonly connects to a switch or router through Ethernet and bridges wireless clients onto the wired LAN.

### Main Functions

- Provides wireless network access.
- Broadcasts one or more wireless network names (SSIDs).
- Connects Wi-Fi clients to the network.
- Supports wireless security and authentication features.

A standalone access point does not normally perform the main routing or DHCP functions of the network. Those functions are usually provided by a router or server.

### Access Point vs. Wireless Router

- **Access Point:** Primarily provides Wi-Fi access to an existing network.
- **Wireless Router:** Typically combines routing, Wi-Fi, and several other networking functions.

A range extender or repeater can extend wireless coverage by relaying the signal.

## 5. Firewall

A **firewall** controls network traffic according to security rules.

It can allow or deny traffic based on factors such as IP addresses, protocols, ports, connection state, and application information, depending on the firewall's capabilities.

### Types

- **Hardware Firewall:** A physical appliance that protects network segments.
- **Software Firewall:** Runs on an individual computer or server.
- **Next-Generation Firewall (NGFW):** May include application awareness, intrusion prevention, and other advanced security features.

### Main Functions

- Allows authorized traffic.
- Blocks traffic prohibited by security policies.
- Restricts access to network services.
- Helps protect internal networks from unwanted connections.

**Key point:** NAT and firewalling are different functions, even though the same router or appliance may perform both.

## 6. NIC (Network Interface Card)

A **Network Interface Card (NIC)** is the hardware or interface that allows a device to communicate over a network.

NICs can support wired Ethernet, wireless networking, or other network technologies.

### Main Functions

- Provides network connectivity.
- Sends and receives network frames or wireless traffic.
- Provides a link-layer interface to the operating system.
- Usually has a MAC address for link-layer communication.

A MAC address is commonly assigned by the manufacturer, although software can sometimes change the address used by an interface.

**Examples:** An Ethernet port on a PC and a Wi-Fi adapter are both network interfaces.

## 7. Hub

A **hub** is a basic network device that repeats incoming signals to its other ports.

Unlike a switch, it does not learn MAC addresses or selectively forward Ethernet frames.

### Key Characteristics

- Operates at the Physical Layer (Layer 1).
- Repeats incoming signals to connected ports.
- Does not maintain a MAC address table.
- Shares bandwidth among connected devices.

Hubs are largely obsolete and have been replaced by switches in modern Ethernet networks.

## 8. Network Bridge

A **bridge** connects network segments at Layer 2.

It learns MAC addresses and forwards frames between segments. A traditional Ethernet switch can be understood as a multiport bridge.

**Key point:** Bridges and Layer 2 switches forward frames using MAC addresses; routers forward packets between IP networks.

## 9. Gateway

A **gateway** is a device or function that connects a system or network to another network or service.

In everyday IP networking, the **default gateway** is the router or Layer 3 device a host sends traffic to when the destination is outside its local subnet.

A gateway can also perform translation between different protocols or systems, depending on its purpose.

**Key point:** A gateway is not necessarily a separate physical device. A router commonly serves as a network's default gateway.

## 10. Other Networking Devices

### Repeater
Regenerates or retransmits signals to extend a connection or its coverage.

### Server
Provides services to other devices, such as web hosting, DNS, DHCP, email, or file sharing.

### Network Attached Storage (NAS)
Provides shared file storage over a network.

### Wireless LAN Controller (WLC)
Centrally manages compatible wireless access points, commonly in enterprise networks.

### Intrusion Detection System (IDS)
Monitors activity to identify suspicious or potentially malicious behavior.

### Intrusion Prevention System (IPS)
Detects suspicious traffic and can block or stop certain unwanted activity.

### Load Balancer
Distributes requests across multiple servers to improve performance and availability.

### Proxy Server
Acts as an intermediary for client requests and may provide filtering, access control, or caching.

### VPN Gateway
Terminates and manages VPN connections between users, offices, or networks.

### Patch Panel
Organizes and terminates network cables. It does not normally forward traffic like a switch.

## 11. How These Devices Work Together

Consider a typical home network:

1. The ISP provides an internet connection through its network.
2. A modem or fiber ONT terminates that connection when required.
3. A router forwards traffic between the home LAN and external networks.
4. A switch connects multiple wired devices.
5. An access point allows wireless devices to join the LAN.
6. A firewall applies traffic-control rules.
7. Each end device uses a network interface to send and receive traffic.

Some home devices combine multiple functions. For example, a single wireless router may contain a router, Ethernet switch, access point, DHCP server, NAT, and firewall.
