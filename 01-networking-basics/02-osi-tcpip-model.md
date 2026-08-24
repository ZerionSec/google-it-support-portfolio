# 02 — OSI Model + TCP/IP Model

This is the next major foundation.

Do not think of OSI as seven things you simply memorize. The real goal is to understand:

> How does data move from one application on one computer to an application on another computer?

The OSI model gives us a way to break that complicated process into understandable layers.

---

## 1. Why Do We Need Networking Models?

Imagine you open a website:

```
You
 ↓
Browser
 ↓
HTTPS
 ↓
TCP/QUIC
 ↓
IP
 ↓
Ethernet/Wi-Fi
 ↓
Router
 ↓
Internet
 ↓
Web Server
```

That's a lot happening. If everything were treated as one giant process, networking would be extremely difficult to design and troubleshoot.

Instead, networking is divided into **layers**. Each layer has a particular responsibility.

Think of it like sending a package:

```
Application
    ↓
"Here's the information I want to send"

Transport
    ↓
"How should the conversation/data delivery work?"

Network
    ↓
"Which network should this go through?"

Data Link
    ↓
"How do I get it across this local link?"

Physical
    ↓
"How do I represent the bits as signals?"
```

That's the fundamental idea behind layered networking.

---

## 2. What Is the OSI Model?

**OSI** means **Open Systems Interconnection**.

The OSI model is a 7-layer reference model used to describe network communication.

The seven layers are:

```
7  Application
6  Presentation
5  Session
4  Transport
3  Network
2  Data Link
1  Physical
```

A common mnemonic is: **All People Seem To Need Data Processing**

But don't rely only on the mnemonic. You need to understand what each layer actually does.

---

## 3. Layer 1 — Physical

Layer 1 deals with the actual transmission of bits through a physical or radio medium.

**Examples:** Copper cable, fiber optic, radio waves, electrical signals, optical signals, connectors, physical interfaces.

At this level, we're dealing with: `101101001011010...`

The bits ultimately have to become physical signals.

**Layer 1 concerns:** Cable, connector, signal, voltage/light/radio, frequency, physical interface, transmission medium, link speed, signal attenuation, interference.

**Typical problems:** Broken cable, disconnected cable, bad connector, damaged fiber, weak wireless signal, electrical interference, wrong transceiver.

If the cable is physically broken, changing DNS settings won't fix it. That's a Layer 1 problem.

---

## 4. Layer 2 — Data Link

Layer 2 is about communication across a local network/link.

This is where you'll encounter:

- MAC addresses
- Ethernet frames

**Important Layer 2 concepts:** MAC addresses, Ethernet, Frames, Switches, VLANs, FCS, Broadcast domains, Switching.

**Example:**

```
PC A
 │
 │ Ethernet frame
 ▼
Switch
 │
 ▼
PC B
```

The switch primarily makes forwarding decisions using Layer 2 information such as MAC addresses.

> Layer 2 = local-link communication.

---

## 5. Layer 3 — Network

Layer 3 is where IP addressing and routing become central.

**Examples:** IPv4, IPv6, Routers, Routing tables.

**Example:**

```
PC
192.168.1.10

       ↓

Router

       ↓

Server
10.10.10.20
```

The Layer 3 question is essentially:

> Where does this packet need to go, and what path should it take?

**Important concepts:** IP addresses, Subnets, Routing, Routers, Network addresses, Next hop, Routing tables.

---

## 6. Layer 4 — Transport

Layer 4 deals with communication between applications/processes across hosts.

The major protocols you'll learn are:

- **TCP** — Transmission Control Protocol
- **UDP** — User Datagram Protocol

You'll also encounter modern protocols such as QUIC (runs over UDP).

Layer 4 introduces concepts such as: Ports, Segmentation/datagrams, Reliability, Ordering, Flow control, Connection management, Retransmission, Congestion control.

**Example:**

```
192.168.1.10:51532
        ↓
142.250.x.x:443
```

Here: IP address = Layer 3, Port = Layer 4.

---

## 7. Layer 5 — Session

Layer 5 is the Session layer. Its conceptual responsibility is managing communication sessions between applications.

Think: Establish session → Maintain session → Exchange information → Terminate session.

**Important real-world point:** Modern TCP/IP networking doesn't cleanly implement the OSI Session layer as a separate protocol layer. Many functions traditionally associated with OSI Layers 5–7 are handled together by application protocols and libraries.

The OSI model is a **reference model**, not a literal diagram of every modern protocol implementation.

---

## 8. Layer 6 — Presentation

The Presentation layer conceptually deals with how data is represented.

Examples of concepts associated with this layer include: Data encoding, Character encoding, Serialization, Compression, Encryption/decryption.

Again, modern TCP/IP stacks don't necessarily contain a distinct "Layer 6 component." For example, TLS provides encryption functionality, but calling TLS simply "Layer 6" is an oversimplification.

---

## 9. Layer 7 — Application

This is the layer closest to the applications that use the network.

**Examples:** HTTP, DNS, SMTP, FTP, SSH, DHCP, SNMP.

**Important:** Application layer does **NOT** mean "the entire browser." The browser is an application. HTTP is an application-layer protocol used by applications.

---

## 10. The Seven Layers Together

| Layer | Name         | Main idea                          | Examples                  |
|-------|--------------|------------------------------------|---------------------------|
| 7     | Application  | Network services for applications  | HTTP, DNS, SMTP           |
| 6     | Presentation | Representation of data             | Encoding, encryption concepts |
| 5     | Session      | Communication sessions             | Session-management concepts |
| 4     | Transport     | End-to-end transport               | TCP, UDP                  |
| 3     | Network      | Logical addressing/routing         | IP, routers               |
| 2     | Data Link    | Local-link communication           | Ethernet, MAC, switches   |
| 1     | Physical     | Signals/bits                       | Copper, fiber, radio      |

---

## 11. Encapsulation & Decapsulation

As data travels **down** the stack, each layer can add information required by that layer. This is called **Encapsulation**.

```
Application data

        ↓

┌────────────────────┐
│ Transport Header    │
│ Application Data    │
└────────────────────┘

        ↓

┌────────────────────────────┐
│ IP Header                   │
│ Transport Header            │
│ Application Data            │
└────────────────────────────┘

        ↓

┌────────────────────────────────────────┐
│ Ethernet Header │ IP │ TCP │ Data │ FCS │
└────────────────────────────────────────┘

        ↓

Bits/signals
```

The receiving computer does the reverse (**Decapsulation**).

---

## 12. PDU — Protocol Data Units

Different layers have different names for the data:

| Layer   | PDU Name              |
|---------|-----------------------|
| 7-5     | Data                  |
| 4       | Segment (TCP) / Datagram (UDP) |
| 3       | Packet                |
| 2       | Frame                 |
| 1       | Bits                  |

```
DATA
 ↓
SEGMENT
 ↓
PACKET
 ↓
FRAME
 ↓
BITS
```

This terminology is extremely important.

---

## 13. OSI vs TCP/IP

The TCP/IP model is more closely associated with the protocol architecture actually used by the Internet.

A common four-layer representation is:

```
TCP/IP

4  Application
3  Transport
2  Internet
1  Link
```

**Mapping:**

```
OSI                         TCP/IP

7 Application ───────┐
6 Presentation ──────┼──→ Application
5 Session ───────────┘

4 Transport ───────────→ Transport

3 Network ─────────────→ Internet

2 Data Link ─────────┐
1 Physical ──────────└──→ Link
```

There are also modern teaching models that use five TCP/IP layers (separating Physical and Data Link).

---

## 14. Why Do Professionals Still Use OSI?

Because OSI gives network professionals a common troubleshooting vocabulary.

Examples:

- "This looks like a Layer 1 problem." → Cable, Signal, Interface, Physical connectivity
- "We're troubleshooting Layer 2." → MAC, Ethernet, VLAN, Switching
- "This is a Layer 3 issue." → IP, Subnet, Routing, Gateway
- "This is Layer 4." → TCP, UDP, Ports, Connections

---

## 15. A Real Troubleshooting Example

Suppose a user says: "I can't access anything."

Don't immediately blame DNS. Start from the bottom:

1. **Layer 1** — Is the cable connected? Is the interface up? Does Wi-Fi have signal?
2. **Layer 2** — Is the switch working? Is the interface in the correct VLAN? Is the MAC being learned?
3. **Layer 3** — Does the PC have an IP? Is the subnet correct? Is the default gateway correct? Can it reach the gateway?
4. **Layer 4** — Can it establish TCP/UDP communication? Is the port reachable?
5. **Layer 7** — Does DNS work? Does HTTP/HTTPS work?

This is how the OSI model becomes useful rather than just something you memorize for an exam.

---

## 16. Detailed PDU Anatomy & Packet Journey

### The Single Most Critical Rule

**IP Addresses (Layer 3) stay the SAME from source to destination.**  
**MAC Addresses (Layer 2) CHANGE at EVERY router hop.**

Analogy: Think of IP as your home address (final destination). Think of MAC as the address of the next post office on the route. The mailman only needs to know where to take the package next. The final home address stays on the package the whole time, but the "next stop" label gets replaced at every sorting facility (router).

### TCP Three-Way Handshake (Before Data Flows)

Before your PC sends application data, TCP requires a connection to be established:

1. **SYN**: PC → Server. "Hi, I want to talk. My initial sequence number is X." (SYN flag = 1)
2. **SYN-ACK**: Server → PC. "I received your X. I also want to talk. My sequence number is Y." (SYN=1, ACK=X+1)
3. **ACK**: PC → Server. "Got your Y. Connection is established!" (ACK=Y+1)

Why 3 steps instead of 2? To prevent old, delayed connection requests from suddenly arriving and confusing the server. Three steps ensure both sides explicitly agree and are ready to send/receive.

---

## 🎥 Recommended Self-Study Resources

- **Professor Messer** — Understanding the OSI Model (N10-009) and TCP/IP Model
- **Practical Networking / NetworkChuck** — Packet journey and encapsulation videos
- **Jeremy's IT Lab** — CCNA Day 1–3 (free, professional-grade)
- **Cisco Networking Academy** — Free Networking Basics course with Packet Tracer activities

### Lab Suggestion

Use Cisco Packet Tracer:

1. Create PC → Switch → Router → Server topology
2. Go into Simulation Mode and send an HTTP request
3. Observe that Source/Destination IP stays the same while MAC addresses rewrite at the router

---

## 🧠 Lesson 02 Checkpoint

**Beginner**

1. What is the OSI model?
2. Why do we divide networking into layers?
3. What is Layer 1 responsible for?
4. What is Layer 2 responsible for?
5. What is Layer 3 responsible for?
6. What is Layer 4 responsible for?
7. What is Layer 7 responsible for?
8. What is the difference between a MAC address and an IP address?
9. What is encapsulation?
10. What is decapsulation?

**Intermediate**

11. What is a frame?
12. What is a packet?
13. What is a segment?
14. What is the relationship between Data → Segment → Packet → Frame → Bits?
15. Why does a router primarily operate at Layer 3?
16. Why does a switch primarily operate at Layer 2?
17. What happens to data as it travels down the OSI stack?
18. What happens when the receiving computer gets the data?

**Challenge**

Imagine: Laptop → Wi-Fi → Access Point → Router → Internet → Web Server

You open `https://example.com`

Explain what happens through the layers and identify Application, Transport, Network, Data Link, and Physical components.
