

# 1. What is a network interface?

A network interface is the connection through which a device sends and receives network traffic.

For example, your laptop might have two network interfaces:

- An Ethernet interface for a wired connection.
- A wireless interface for Wi-Fi.

<img width="2048" height="1375" alt="image" src="https://github.com/user-attachments/assets/9a2cf29f-4928-49ee-84ac-cbb875595b77" />


**Ethernet interface** : Connects to a wired network through an Ethernet cable.

<img width="1600" height="1067" alt="image" src="https://github.com/user-attachments/assets/64c78877-4367-4325-b7a0-2c47e4550d7d" />


**Wireless interface** : Connects to a Wi-Fi network using radio signals.

A network interface is often provided by a NIC (Network Interface Card). It might be built into the motherboard rather than being a separate card.

<img width="678" height="688" alt="image" src="https://github.com/user-attachments/assets/a69a8347-5599-4b2c-a7f4-0587934744e2" />


### How to read an interface name

For example, `GigabitEthernet0/1` tells you that you're looking at a Gigabit Ethernet interface.

On a switch, `FastEthernet0/1` usually means FastEthernet port 1 on that device. On a router, interface numbering depends on the device model.

You don't need to memorize every naming convention yet. Learn to identify the interface type and the port to which a cable should connect.

# 2. What is a network cable?

A network cable provides a physical path for signals to travel between devices. Different cables are designed for different types of connections.

## The cables you should know




1\. Copper straight-through Ethernet cable

<img width="1200" height="900" alt="image" src="https://github.com/user-attachments/assets/5a2aa096-61ad-494a-82d9-88c89ce33b9e" />

Used for common Ethernet connections, such as PC to switch and router to switch. It is one of the main cables you'll use in your Packet Tracer labs.


2\. Copper crossover cable

<img width="800" height="450" alt="image" src="https://github.com/user-attachments/assets/2f977632-be81-4e9c-8d18-e987b11d209d" />

Traditionally used to connect similar Ethernet interfaces directly, such as switch to switch or PC to PC. Modern equipment often supports Auto-MDI/MDIX, which can automatically accommodate either cable type. Packet Tracer may also handle some connections differently depending on the device.


3\. Fiber-optic cable

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/f17519da-5cb0-4cce-b261-92ee319d64cb" />

Carries data using light. Used for high-speed connections and longer-distance links. Fiber requires compatible optical interfaces or transceivers at both ends.

4\. Serial cable

<img width="691" height="566" alt="image" src="https://github.com/user-attachments/assets/9d9fde3d-dd83-4279-8cf1-94898a615863" />

Used with supported router interfaces in some simulated WAN connections.

You may encounter DCE and DTE ends in Packet Tracer. The exact configuration depends on the lab and router model.


5\. Console cable

<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/0bdb1156-6508-4024-902d-793ac94638c4" />

Connects a computer's terminal interface to a network device's console port so you can configure it locally. It is not a cable for ordinary Ethernet communication. You may also encounter coaxial cables, which are used by cable internet systems and other technologies. You don't need to configure a coaxial internet connection for this basic Packet Tracer lab.

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

<img width="2000" height="1500" alt="image" src="https://github.com/user-attachments/assets/87fe60f4-16f2-4045-9f0f-bd1206ebef11" />

An Ethernet port is the physical socket into which you connect an Ethernet cable. For example, a switch might have these ports:

- `FastEthernet0/1`
- `FastEthernet0/2`
- `FastEthernet0/3`
- `GigabitEthernet0/1`

If you connect a PC to `FastEthernet0/1`, that tells you which switch port the PC is connected to. This becomes useful later when you learn MAC address tables, VLANs, STP, and switch troubleshooting.

## Port vs. interface

People often use these words interchangeably in basic networking.

- Port: Often means the physical socket or connection point.
- Interface: The network interface through which communication occurs. It may refer to a physical interface or a logical interface, depending on the context.

For this lab, you can treat `FastEthernet0/1` as the particular physical network connection you select on a switch.

<img width="695" height="401" alt="image" src="https://github.com/user-attachments/assets/b2fa9808-75e5-4585-98d7-cecd7710013e" />


# 6. Speed, duplex and cable length

You don't need to master these topics today, but learn the basic definitions.

Speed is how fast an interface can transmit data. For example, 100 Mbps and 1 Gbps are different Ethernet speeds. The actual link rate depends on the capabilities and configuration of both ends.

Duplex describes whether an Ethernet connection can send and receive simultaneously.

- Half-duplex: sends or receives at a time.
- Full-duplex: can send and receive simultaneously.

Modern switched Ethernet links generally use full-duplex operation. Duplex mismatches can cause poor performance and errors.

Cable length: copper twisted-pair Ethernet commonly supports up to 100 metres per channel under the applicable cabling specifications. Fiber can support much longer distances, depending on the fiber type, transceivers, and link design.

You don't need to calculate cable lengths in this lab. Just understand that cables and interfaces have technical limits.

