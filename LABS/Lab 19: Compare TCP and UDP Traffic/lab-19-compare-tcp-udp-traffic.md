# Lab 19: Compare TCP and UDP Traffic

## Objective

Understand the differences between TCP and UDP, how they transmit data, and when each transport-layer protocol is used.

## 1. What Are TCP and UDP?

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are transport-layer protocols.

They allow applications on different devices to communicate over a network.

- **TCP:** Connection-oriented and provides reliable, ordered data delivery.
- **UDP:** Connectionless and sends data without guaranteeing delivery or order.

Both use port numbers to identify the sending and receiving applications.

## 2. TCP (Transmission Control Protocol)

TCP establishes a connection before transferring data.

### Main Features

- Connection-oriented communication.
- Reliable data delivery.
- Keeps data in the correct order.
- Detects missing or corrupted data and retransmits missing data when necessary.
- Uses acknowledgments (ACKs) to confirm received data.
- Provides flow control and congestion control.
- Has more protocol overhead than UDP.

### TCP Three-Way Handshake

TCP establishes a connection using three messages:

1. **SYN:** Client requests a connection.
2. **SYN-ACK:** Server acknowledges the request and responds.
3. **ACK:** Client acknowledges the server's response.

The connection is then established, and data transfer can begin.

### Example

When a client connects to a traditional TCP-based web service, TCP establishes the connection before transferring application data.

TCP is commonly used for:

- File transfers (FTP)
- Email transmission (SMTP)
- Remote administration (SSH)
- Traditional HTTP and HTTPS connections carried over TCP

Note: Modern HTTP/3 uses QUIC over UDP instead of TCP.

## 3. UDP (User Datagram Protocol)

UDP sends individual datagrams without establishing a connection first.

### Main Features

- Connectionless communication.
- No guaranteed delivery.
- No guaranteed ordering.
- No built-in retransmission of lost datagrams.
- No built-in flow control or congestion control equivalent to TCP.
- Smaller header and lower protocol overhead.
- Suitable for applications that prioritize low latency.

Applications can implement their own reliability mechanisms when needed.

### Example

A DNS client commonly sends a query using UDP and receives a response from the DNS server.

UDP is commonly used for:

- DNS queries
- DHCP
- VoIP and real-time communication
- Online gaming
- Live audio and video streaming
- TFTP

Some applications use TCP when necessary, such as DNS in certain circumstances.

## 4. TCP vs UDP

| Feature | TCP | UDP |
|---|---|---|
| Communication | Connection-oriented | Connectionless |
| Connection setup | Three-way handshake | No handshake required |
| Delivery guarantee | Reliable delivery mechanisms | No delivery guarantee |
| Ordering | Preserves byte-stream order | No ordering guarantee |
| Retransmission | Built-in | Not built-in |
| Acknowledgments | Yes | No built-in ACK mechanism |
| Flow control | Yes | No built-in flow control |
| Congestion control | Yes | No built-in congestion control |
| Header size | Minimum 20 bytes | 8 bytes |
| Overhead | Higher | Lower |
| Common uses | SSH, FTP, SMTP, TCP-based web traffic | DNS, DHCP, VoIP, gaming |

## 5. TCP and UDP Port Numbers

Port numbers help the operating system deliver transport-layer data to the correct application.

Common examples:

| Service | Common Port | Transport |
|---|---:|---|
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP (traditional HTTPS); HTTP/3 uses QUIC over UDP |
| SSH | 22 | TCP |
| FTP control | 21 | TCP |
| SMTP | 25 | TCP |
| DNS | 53 | UDP and TCP |
| DHCP server | 67 | UDP |
| DHCP client | 68 | UDP |
| TFTP | 69 | UDP |

A port number alone does not guarantee which application is running on it; services can be configured to use different ports.

## 6. How to Choose Between TCP and UDP

Choose TCP when the application needs reliable, ordered delivery.

Examples:
- Downloading a file
- Sending email
- Managing a server remotely

Choose UDP when minimizing delay or protocol overhead is important and the application can tolerate loss or handle reliability itself.

Examples:
- Voice calls
- Real-time gaming
- Many DNS queries

UDP is not automatically faster in every situation, and TCP is not always the best choice. The right protocol depends on the application's requirements.

## 7. How TCP and UDP Traffic Travels

When an application sends data:

1. The application creates data to send.
2. TCP or UDP adds its transport-layer header, including source and destination ports.
3. IP adds the network-layer header with source and destination IP addresses.
4. Ethernet or another link-layer technology carries the packet across the local network.
5. The receiving device processes the headers and delivers the data to the appropriate application.

TCP data is carried in TCP segments. UDP data is carried in UDP datagrams.

Routers forward IP packets, while switches forward Ethernet frames within a Layer 2 network.

## Key Takeaway

TCP provides reliable, ordered data delivery using acknowledgments and retransmissions. UDP sends datagrams with lower overhead but does not guarantee delivery or ordering. Applications choose the protocol based on their communication requirements.
