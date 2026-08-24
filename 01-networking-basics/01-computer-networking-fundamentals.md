# 01 — Computer Networking Fundamentals

This is the foundation layer of networking. Before learning subnetting, VLANs, routing, Wireshark, firewalls, or cybersecurity networking, you should be comfortable with these concepts.

I’ll explain each one in this order:

**What it is → why it exists → how it works → example → important details → common misconception.**

---

## 1. What Is a Computer Network?

### Simple definition

A computer network is a collection of devices connected together so they can communicate and exchange data or share resources.

**Example:**

```
Internet
                │
             Router
          ┌────┼────┐
          │     │     │
       Laptop Phone Printer
```

These devices form a network because they can communicate through networking technologies.

### What can a network do?

A network can allow devices to:

- Exchange files
- Access websites
- Send messages
- Share printers
- Share Internet access
- Access databases
- Run applications
- Make voice/video calls
- Access cloud services
- Monitor devices
- Provide centralized services

### What makes communication possible?

Several components work together:

```
Devices
   ↓
Network Interfaces
   ↓
Communication Media
   ↓
Protocols
   ↓
Addresses
   ↓
Networking Devices
   ↓
Services
```

For example:

```
Laptop
   ↓
Wi-Fi NIC
   ↓
Wi-Fi
   ↓
Router
   ↓
ISP
   ↓
Internet
   ↓
Web Server
```

---

## 2. LAN — Local Area Network

**LAN = Local Area Network**

A LAN connects devices within a relatively limited area.

**Examples:**

- Home
- Classroom
- Computer laboratory
- Office
- Building

**Example:**

```
Router
                │
          ┌────┼────┐
          │     │     │
         PC    PC    Printer
```

This could be a LAN.

### Characteristics

LANs generally have:

- Relatively short geographic scope
- High-speed local communication
- Ethernet or Wi-Fi
- Switches and access points
- Private addressing in many environments

### Example

Your home:

```
Phone ───┐
Laptop ───┤
TV ──────┼── Wi-Fi Router
Console ──┤
PC ──────┘
```

That's a typical home LAN.

**Important:** LAN doesn't necessarily mean wired. A WLAN is a wireless LAN.

---

## 3. WAN — Wide Area Network

**WAN = Wide Area Network**

A WAN connects networks across a large geographic area.

For example:

```
Office A
   │
   │
 ISP/WAN
   │
   │
Office B
```

A company might have:

```
Manila Office
      │
      │ WAN
      │
Cebu Office
      │
      │ WAN
      │
Davao Office
```

WAN technologies can include:

- ISP connections
- MPLS
- Leased lines
- VPNs
- Internet-based connectivity
- Cellular networks
- Other carrier technologies

### LAN vs WAN

| Feature          | LAN                          | WAN                              |
|------------------|------------------------------|----------------------------------|
| Scope            | Local                        | Large geographic area            |
| Example          | Home network                 | Company connecting cities        |
| Typical latency  | Lower                        | Usually higher                   |
| Ownership        | Often one organization/person| Often involves carriers/ISPs     |
| Technologies     | Ethernet/Wi-Fi               | Fiber, MPLS, VPN, carrier networks |

---

## 4. MAN — Metropolitan Area Network

**MAN = Metropolitan Area Network**

A MAN is generally used to describe a network spanning a city or metropolitan area.

Conceptually:

```
Building A ───┐
              │
Building B ───┼── Metropolitan Network
              │
Building C ───┘
```

Historically, MAN was a common classification between LAN and WAN.

Today, the distinction isn't always rigid because modern networks can use many different technologies and architectures.

**Example:** A university might have multiple campuses throughout a city connected through a metropolitan network.

---

## 5. PAN — Personal Area Network

**PAN = Personal Area Network**

This is a small network around an individual.

**Examples:**

```
Phone
       /     \
  Bluetooth  Wi-Fi
     /         \
Earbuds       Watch
```

Examples include:

- Bluetooth headphones
- Smartwatch connected to phone
- Keyboard connected to laptop
- Personal hotspot
- USB-connected devices

**The key idea:** PAN = very small personal-scale network.

---

## 6. The Network Scope Hierarchy

A useful mental model:

```
PAN
 ↓
LAN
 ↓
MAN
 ↓
WAN
```

But don't think these are strict technical boundaries. They're primarily descriptive classifications based on geographic scope and architecture.

---

## 7. Internet vs Intranet

This distinction is extremely important.

### Internet

The Internet is the global interconnected system of networks that communicate using Internet technologies and protocols.

Conceptually:

```
Network A ──┐
Network B ──┼── Internet
Network C ──┤
Network D ──┘
```

It's not one single physical network. It's a **network of networks**.

### Intranet

An intranet is a private network or collection of private resources used within an organization.

**Example:**

```
Company Employees
        │
        ▼
   Company Network
        │
   ┌───┼────┐
   ▼    ▼     ▼
 HR   Payroll Internal Apps
```

Employees might access `intranet.company.local` or an internal application.

### Internet vs Intranet

| Feature | Internet                  | Intranet                     |
|---------|---------------------------|------------------------------|
| Scope   | Global                    | Organization/private         |
| Access  | Generally public          | Restricted                   |
| Users   | Potentially anyone        | Authorized users             |
| Example | Public website            | Internal company portal      |

**Important misconception:** An intranet doesn't necessarily mean the network is completely disconnected from the Internet. A company can have Internet access while using firewalls and access controls to protect internal resources.

---

## 8. Client vs Server

This is one of the most important networking concepts.

### Client

A client requests a service.

**Example:**

```
Browser
   │
   │ Request
   ▼
Web Server
```

Your browser is acting as a client.

### Server

A server provides a service.

```
Client
  │
  │ Request
  ▼
Server
  │
  │ Response
  ▼
Client
```

Examples of servers: Web server, DNS server, File server, Database server, Mail server, DHCP server.

**Important:** "Server" doesn't necessarily mean a giant computer. A server is fundamentally a **role**: providing a service. A single computer can potentially be a client for one service and a server for another.

---

## 9. Peer-to-Peer

**P2P = Peer-to-Peer**

In a peer-to-peer architecture, devices can communicate directly and potentially provide services to one another.

```
PC A ───── PC B
 │           │
 └─────┴─────┘
       │
      PC C
```

There isn't necessarily one centralized server providing everything. Each peer can potentially act as both Client + Server depending on the communication.

### Client-Server vs P2P

| Feature        | Client-Server              | P2P                          |
|----------------|----------------------------|------------------------------|
| Central server | Usually yes                | Not necessarily              |
| Control        | Centralized                | Distributed                  |
| Management     | Easier centrally           | More distributed             |
| Scalability    | Depends on architecture    | Can distribute workload      |
| Example        | Web applications           | Some decentralized/file-sharing systems |

Modern systems can also be hybrid.

---

## 10. Network Topologies

A network topology describes how network devices are arranged or interconnected.

- **Physical topology**: How devices/cables are physically arranged.
- **Logical topology**: How data actually flows through the network.

These don't always have to be identical.

### Star Topology

```
PC
              │
              │
PC ─────── Switch ───── PC
              │
              │
           Printer
```

The central device is commonly a switch in modern Ethernet networks.

**Advantages:** Easy to manage, easy to expand, one endpoint cable failure usually affects only that device, easier troubleshooting.

**Disadvantages:** The central device is critical. If the central switch fails, many connected devices lose connectivity.

Most modern wired LANs are physically organized around switches, making star-like topologies extremely common.

### Bus Topology

```
PC ─── PC ─── PC ─── PC
      Shared Bus
```

Older Ethernet technologies used bus-like physical arrangements. Mostly important today as a historical and conceptual topology.

### Ring Topology

```
PC ─── PC
│       │
PC ─── PC
```

Each device connects to neighboring devices. Some technologies have used dual rings for resilience.

### Mesh Topology

In a mesh topology, devices have multiple connections to other devices.

**Full mesh:** Every device connects to every other device.

```
      A
     /|\
    / | \
   B--|--C
    \ | /
     \|/
      D
```

Provides redundancy. For *n* devices, a full mesh requires:

$$\frac{n(n-1)}{2}$$

connections.

### Hybrid Topology

A hybrid topology combines different topology types. Real networks rarely fit perfectly into one textbook topology.

---

## 11. Performance Concepts

### Bandwidth

Bandwidth describes the capacity of a communication link. Usually expressed in bits per second (Mbps, Gbps).

Think of bandwidth like the width of a road. More bandwidth generally means the link can carry more data per unit time.

**Important:** Bandwidth does not automatically mean the user will actually receive that data rate.

### Throughput

Throughput is the amount of data actually successfully transferred over a network during a given period.

Example: Link bandwidth = 1 Gbps, measured throughput = 700 Mbps.

Possible causes for lower throughput: Protocol overhead, congestion, packet loss, network equipment limitations, server limitations, Wi-Fi interference, traffic shaping, etc.

**Bandwidth = potential capacity**  
**Throughput = actual achieved rate**

### Latency

Latency is the time it takes for data to travel from one point to another (usually measured in milliseconds).

Lower latency generally means faster response time. Important for gaming, voice, video calls, interactive applications.

### Jitter

Jitter refers to variation in packet delay. Especially important for real-time applications (voice calls, video calls, online gaming, live streaming).

### Packet Loss

Packet loss occurs when packets fail to reach their destination. Causes include congestion, faulty hardware, wireless interference, poor signal, buffer exhaustion, etc.

Effects: Slow applications, retransmissions, video/voice problems, TCP performance degradation.

---

## 12. Duplex

**Half-Duplex:** Communication can occur in both directions, but not simultaneously (like a walkie-talkie).

**Full-Duplex:** Communication can occur in both directions simultaneously (like a telephone conversation).

Modern switched Ethernet links commonly operate in full-duplex mode.

---

## 13. Traffic Delivery Models

### Unicast
One sender → one receiver

```
A ─────────→ B
```

### Broadcast
One sender → all devices within the relevant broadcast domain

```
      ┌→ B
      │
A ────┼→ C
      │
      └→ D
```

### Multicast
One sender → selected group of receivers

```
      ┌→ B ✓
      │
A ────┼→ C ✓
      │
      └→ D ✗
```

IPv4 multicast uses addresses from 224.0.0.0 – 239.255.255.255.

### Anycast
The same service address is associated with multiple possible destinations, and routing directs the client toward an appropriate (usually topologically nearest) instance.

Widely used for DNS, content delivery, and global services.

---

## 🧠 Fundamentals Checkpoint

Before moving to OSI Model + TCP/IP Model, answer these without looking back:

1. What is the difference between a LAN and WAN?
2. What is the difference between Internet and intranet?
3. Can one computer be both a client and a server? Why?
4. What is the main difference between client-server and P2P?
5. Why is star topology common in modern LANs?
6. What is the difference between bandwidth and throughput?
7. A connection has high bandwidth but very high latency. What does that mean?
8. What is jitter?
9. What happens when packets are lost?
10. What is the difference between half-duplex and full-duplex?
11. What is the difference between unicast, multicast, broadcast, and anycast?
12. Your phone is connected to your home Wi-Fi. Is that a LAN, WAN, or both? Explain.
13. Why does a router matter when your destination is outside your local network?
14. Why isn't "server" necessarily the name of a specific type of physical computer?

---

## Learning Path

```
01 Fundamentals
       ↓
02 OSI / TCP-IP
       ↓
03 Ethernet
       ↓
04 MAC Addressing
       ↓
05 IPv4
       ↓
06 Subnetting
       ↓
07 IPv6
       ↓
08 ARP
       ↓
09 Switching
       ↓
10 VLAN
       ↓
11 Routing
       ↓
12 TCP / UDP
       ↓
13 DNS / DHCP
       ↓
14 NAT
       ↓
15 Wireless
       ↓
16 Network Security
       ↓
17 Troubleshooting
       ↓
18 Practical Labs
       ↓
19 Network Design
       ↓
20 Advanced Networking
```

We start with **01 — Fundamentals**.
