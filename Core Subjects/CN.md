# Computer Networks

<details>
  <summary>01: Introduction to Computer Networks</summary>

### Types of Networks

Networks are primarily categorized based on their geographical scope.


| Network Type | Scope | Example | Key Characteristics |
| :-- | :-- | :-- | :-- |
| **LAN** (Local Area Network) | Small area (single room, office building, campus) | An office network or your home Wi-Fi network. | High speed, low latency, privately owned. |
| **MAN** (Metropolitan Area Network) | City-wide | A cable TV network spanning a city. | Spans a larger area than a LAN but smaller than a WAN. |
| **WAN** (Wide Area Network) | Large geographical area (country, continent) | The Internet itself is the largest WAN. | Lower speed, higher latency, often relies on public infrastructure. |

### Interconnected Networks (IMP)

Understanding the distinction between these network types is a common interview topic.

* **Internet:** A global system of interconnected computer networks that uses the TCP/IP protocol suite to communicate between networks and devices. It is a public, global WAN.
* **Intranet:** A private network contained within an enterprise. It consists of many interlinked local area networks and also uses TCP/IP. It is used for internal company communication, sharing information, and hosting internal applications.
* **Extranet:** An intranet that can be partially accessed by authorized outside users (e.g., suppliers, customers, partners). It enables business-to-business (B2B) communication.


### Network Topologies

Topology defines the arrangement of network devices and the paths used for data transmission. It is divided into physical and logical topology.

* **Physical Topology:** The physical layout of devices, cables, and other components.
  * *Analogy:* Think of it as the road map of a city, showing how houses (nodes) and streets (cables) are physically laid out.
* **Logical Topology:** The path that data signals take through the network.
  * *Analogy:* This is like the specific bus route a mail truck follows to deliver mail, which may not use every single street.


### Physical Topologies (IMP)

* **Bus Topology:** All devices are connected to a single central cable, called the bus or backbone.
  * **Pros:** Simple, inexpensive.
  * **Cons:** A single cable failure can take down the entire network. Performance degrades as more devices are added.
* **Star Topology:** All devices are connected to a central hub or switch. **(IMP)**
  * **Pros:** Easy to install and manage. A single node failure does not affect the rest of the network.
  * **Cons:** If the central device fails, the entire network fails.
  * **Best Practice:** This is the most common topology used in modern LANs (e.g., Ethernet switches).
* **Ring Topology:** Each device is connected to exactly two other devices, forming a circular pathway for signals.
  * **Pros:** Performs better than a bus topology under heavy load.
  * **Cons:** A failure in one node or cable can break the loop and take down the entire network.
* **Mesh Topology:** Every device is connected to every other device.
  * **Pros:** Highly fault-tolerant and robust. If one link fails, data can be redirected.
  * **Cons:** Very expensive and complex to install and manage due to the amount of cabling required.
* **Tree Topology:** A hybrid topology that combines characteristics of bus and star topologies. It consists of groups of star-configured workstations connected to a linear bus backbone cable.
* **Hybrid Topology:** A combination of two or more different topologies.
  * **Common Pitfall:** Students often confuse Tree and Hybrid. A Tree is a specific type of Hybrid topology, but not all Hybrids are Trees. A common hybrid is a Star-Bus network.


</details>


---

<details>
  <summary>02: Networking Models</summary>

### Networking Models

Networking models provide a standardized framework to understand how different networking protocols and devices interact. They break down the complex process of network communication into smaller, manageable layers.

### OSI Model (Open Systems Interconnection) (IMP)

The OSI model is a **conceptual framework** used to understand and standardize the functions of a telecommunication or computing system without regard to its underlying internal structure and technology. It consists of 7 layers.

* **Analogy:** Think of the OSI model as building a letter and sending it via a postal service. Each layer adds a piece of information (like an address, stamp, or envelope) needed for successful delivery.

| Layer | Name | PDU | Primary Function(s) | Real-World Example |
| :-- | :-- | :-- | :-- | :-- |
| **7** | **Application** | Data | Provides network services directly to user applications. | HTTP, FTP, SMTP, DNS. Your web browser. |
| **6** | **Presentation** | Data | Translates, encrypts, and compresses data. | JPEG, GIF, SSL/TLS encryption. |
| **5** | **Session** | Data | Establishes, manages, and terminates sessions between applications. | APIs, NetBIOS. Login/logout procedures. |
| **4** | **Transport** | Segment (TCP) / Datagram (UDP) | Provides reliable or unreliable delivery; performs error correction before re-transmit. **(IMP)** | TCP, UDP. |
| **3** | **Network** | Packet | Moves packets from source to destination; provides logical addressing and routing. **(IMP)** | IP (IPv4/IPv6), ICMP. Routers operate here. |
| **2** | **Data Link** | Frame | Organizes bits into frames; provides hop-to-hop delivery and physical addressing. | Ethernet, MAC Addresses. Switches operate here. |
| **1** | **Physical** | Bit | Transmits raw bit stream over the physical medium. | Cables (Ethernet, Fiber), Hubs, Voltage levels. |

*Mnemonic to remember the layers (from top to bottom):* **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing.

### TCP/IP Model

The TCP/IP model is a more practical and widely implemented model, forming the basis of the modern internet. It is less rigid and consists of 4 layers.


| Layer | Name | OSI Equivalent | Key Protocols |
| :-- | :-- | :-- | :-- |
| **4** | **Application** | Application, Presentation, Session | HTTP, FTP, SMTP, DNS, SNMP |
| **3** | **Transport** | Transport | TCP, UDP |
| **2** | **Internet** | Network | IP, ICMP, ARP |
| **1** | **Network Access / Link** | Data Link, Physical | Ethernet, Wi-Fi, MAC Address |

### OSI vs. TCP/IP Model Comparison (IMP)

This is a very common interview question.


| Feature | OSI Model | TCP/IP Model |
| :-- | :-- | :-- |
| **Layers** | 7 layers | 4 layers |
| **Development** | Developed by ISO as a theoretical model. | Developed by the Department of Defense (DoD) as a practical, implementation-focused model. |
| **Approach** | Vertical approach; layers are well-defined and have distinct functions. | Horizontal approach; less rigid boundaries. |
| **Usage** | Used as a **reference model** for teaching and understanding network functions. | Used for the **actual implementation** of the standard internet protocols. |
| **Protocol Dependency** | The model was defined before the protocols. | The protocols were defined first, and the model was created to describe them. |

* **Common Pitfall:** Confusing the two models. Remember, OSI is the *idealized, 7-layer theoretical guide*, while TCP/IP is the *practical, 4-layer model that runs the internet*. The TCP/IP model is more relevant in practice, but the OSI model is crucial for understanding concepts.


</details>

---

<details>
  <summary>03: Networking Fundamentals and Basics</summary>

### Network Cabling and Connectors

Cables are the physical medium through which data is transmitted.

* **Twisted-Pair Cable:**
  * **UTP (Unshielded Twisted Pair):** Most common type of cable used in LANs (e.g., Cat5e, Cat6). It's inexpensive and flexible. The twists help reduce electromagnetic interference (EMI).
  * **STP (Shielded Twisted Pair):** Contains an extra layer of metallic shielding to further protect against EMI. Used in environments with high interference.
  * **Connectors:** Use **RJ45** connectors.
* **Fiber Optic Cable:** Transmits data as pulses of light.
  * **Pros:** Immune to EMI, supports very high bandwidth and long distances.
  * **Cons:** More expensive and fragile than twisted-pair.
  * **Connectors:** Common types include SC, ST, and LC.
* **Straight-Through vs. Crossover Cable (IMP):**
  * **Straight-Through:** Used to connect *dissimilar* devices (e.g., PC to Switch, Router to Switch). The pinout is the same on both ends.
  * **Crossover:** Used to connect *similar* devices (e.g., PC to PC, Switch to Switch). The send and receive pins are swapped.
  * **Best Practice:** Modern devices often support **Auto-MDI/MDI-X**, which automatically detects the cable type and adjusts, making crossover cables largely obsolete for modern hardware.


### Network Devices (IMP)

This is a critical topic for interviews. Understanding the OSI layer at which each device operates is key.


| Device | OSI Layer | Function | Addressing Used | Key Feature |
| :-- | :-- | :-- | :-- | :-- |
| **Hub** | Layer 1 (Physical) | Connects multiple devices in a LAN. | N/A | Broadcasts incoming traffic to all ports. Creates a single collision domain. (Obsolete) |
| **Switch** | Layer 2 (Data Link) | Connects devices in a LAN and forwards traffic intelligently. | **MAC Address** | Learns MAC addresses of connected devices and forwards frames only to the destination port. Each port is a separate collision domain. |
| **Router** | Layer 3 (Network) | Connects different networks and forwards packets between them. | **IP Address** | Makes routing decisions to find the best path to a destination network. Each interface is a separate broadcast domain. |
| **Bridge** | Layer 2 (Data Link) | Connects two separate LAN segments into one. | **MAC Address** | Similar to a switch but with fewer ports. Largely replaced by switches. |
| **Gateway** | All Layers | Connects networks with different protocols/architectures. | N/A | Acts as a translator. E.g., an email gateway connecting an internal mail system to the internet. |

### Ethernet Frame Structure (IMP)

An Ethernet frame is the PDU (Protocol Data Unit) at the Data Link Layer. This is what data looks like when it travels over an Ethernet cable.

**Ethernet II Frame Structure:**
`[ Preamble (7B) | SFD (1B) | Dest MAC (6B) | Src MAC (6B) | EtherType (2B) | Payload (46-1500B) | FCS (4B) ]`

* **Preamble \& SFD (Start Frame Delimiter):** Used for synchronization between devices.
* **Destination \& Source MAC:** The physical addresses of the receiving and sending devices.
* **EtherType:** Identifies the protocol of the payload (e.g., `0x0800` for IPv4, `0x86DD` for IPv6).
* **Payload:** The actual data from the upper layers (e.g., an IP packet). The **MTU (Maximum Transmission Unit)** for standard Ethernet is 1500 bytes.
* **FCS (Frame Check Sequence):** Used for error detection (using CRC - Cyclic Redundancy Check).


### ARP (Address Resolution Protocol) (IMP)

ARP is the glue between Layer 2 and Layer 3. It resolves an IP address to a physical MAC address on a local network.

* **Analogy:** You know your friend's name (IP address), but you don't know their house number (MAC address) on a specific street (LAN). You shout on the street (ARP broadcast), "Who is John Doe?" and he replies with his house number (ARP reply).

**How it works:**

1. **ARP Request:** A host sends a **broadcast** message to every device on the LAN, asking, "Who has this IP address (`192.168.1.10`)?"
2. **ARP Reply:** The device that owns that IP address responds with a **unicast** message directly to the original host, saying, "I have that IP. My MAC address is `AA:BB:CC:11:22:33`."
3. **ARP Cache:** The original host stores this IP-to-MAC mapping in its ARP cache for future use.

**Example Command:**
You can view your computer's ARP cache with this command:

```bash
# Windows or Linux/macOS
arp -a
```

The output will show a list of IP addresses and their corresponding MAC addresses.

* **Common Pitfall:** Forgetting that the ARP Request is a broadcast, while the ARP Reply is a unicast.


### NAC (Network Access Control)

NAC is a security solution that enforces policies to control which devices can access a network.

* **Purpose:** To prevent unauthorized or non-compliant devices from connecting.
* **How it works:** Before granting network access, NAC checks the device's "posture" or "health." This can include:
  * User authentication (username/password).
  * Checking for up-to-date antivirus software.
  * Ensuring the operating system is patched.
* **Real-World Example:** Many corporate and university Wi-Fi networks use NAC. When you first connect, you are redirected to a login portal (**Captive Portal**) before you can access the internet. This is a form of NAC using the **IEEE 802.1X** standard.


</details>

---

<details>
  <summary>04: Network Protocols & Communications</summary>

### Network Protocols

A **network protocol** is a set of established rules that dictates how data is formatted, transmitted, and received between network devices. Without protocols, devices could not understand each other.

* **Analogy:** Protocols are like a shared language and set of conversational rules (e.g., grammar, when to speak, how to greet someone) that two people use to have a coherent conversation.


### Application Layer Protocols (IMP)

These protocols provide services directly to user applications. Knowing their function and default ports is crucial for interviews.


| Protocol | Full Name | Port(s) | Function \& Key Concepts |
| :-- | :-- | :-- | :-- |
| **HTTP/HTTPS** | Hypertext Transfer Protocol (Secure) | 80 (HTTP), 443 (HTTPS) | The foundation of the World Wide Web. Used for loading web pages. HTTPS adds a layer of security using **TLS/SSL** for encryption and authentication. |
| **FTP** | File Transfer Protocol | 20 (Data), 21 (Control) | Used for transferring files between a client and a server. **(IMP)** A common question is about its two modes: **Active Mode** (server initiates data connection to client) and **Passive Mode** (client initiates data connection to server). Passive mode is more firewall-friendly. |
| **SMTP** | Simple Mail Transfer Protocol | 25 | The standard protocol for sending emails from a client to a mail server (email submission) and between mail servers. |
| **SNMP** | Simple Network Management Protocol | 161 (Agent), 162 (Manager) | Used for managing and monitoring network devices like routers, switches, and servers. An SNMP Manager can query an SNMP Agent on a device for information (e.g., CPU load, traffic stats). |

### Connection-Oriented vs. Connectionless Protocols (IMP)

This is a fundamental concept, centered on the two main Transport Layer protocols: TCP and UDP.

* **Connection-Oriented (TCP - Transmission Control Protocol):**
  * Establishes a dedicated connection before data is sent.
  * **Analogy:** A phone call. You must establish a connection (dial and wait for the person to pick up) before you can start talking. The conversation is reliable and in order.
  * **Features:** Reliable, ordered delivery, error checking, and flow control.
  * **Three-Way Handshake (IMP):** TCP uses this process to establish a connection.

1. **SYN:** The client sends a SYN (synchronize) packet to the server.
2. **SYN-ACK:** The server replies with a SYN-ACK (synchronize-acknowledge) packet.
3. **ACK:** The client sends an ACK (acknowledge) packet back to the server, and the connection is established.
  * **Use Cases:** Web browsing (HTTP), email (SMTP), file transfers (FTP).
* **Connectionless (UDP - User Datagram Protocol):**
  * Sends data without establishing a prior connection.
  * **Analogy:** Sending a postcard. You just write it and drop it in the mailbox. There's no guarantee it will arrive, in what order, or that it won't be damaged.
  * **Features:** Fast, lightweight, low overhead. No reliability or ordering guarantees.
  * **Use Cases:** Video/audio streaming (VoIP), online gaming, DNS queries.


### Comparison: TCP vs. UDP (IMP)

| Feature | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :-- | :-- | :-- |
| **Connection** | Connection-oriented | Connectionless |
| **Reliability** | **Reliable.** Guarantees delivery of data. | **Unreliable.** No guarantee of delivery. |
| **Ordering** | Data is delivered in the correct sequence. | Data may arrive out of order. |
| **Speed** | Slower due to overhead (handshake, acknowledgements). | Faster due to minimal overhead. |
| **Header Size** | 20 bytes (plus options) | 8 bytes |
| **Use Case** | When reliability is critical (web, email, file transfer). | When speed is critical and some data loss is acceptable (streaming, DNS, gaming). |

* **Common Pitfall:** Saying UDP is "bad" because it's unreliable. UDP is not bad; it's designed for different use cases where the trade-off of speed for reliability is acceptable and often desired. For example, in a video call, receiving a slightly late video frame is useless, so it's better to just drop it and show the next one (UDP's behavior) rather than halting the stream to re-transmit it (TCP's behavior).


</details>

---

<details>
  <summary>05: IP Addressing & Subnetting</summary>

### IP Addressing (IPv4 and IPv6)

An **IP (Internet Protocol) address** is a unique numerical label assigned to each device connected to a computer network that uses the Internet Protocol for communication. It serves two main functions: host identification and location addressing.

* **Public vs. Private IP Addresses (IMP):**
  * **Public IP:** Routable on the internet, assigned by an ISP. Must be globally unique.
  * **Private IP:** Used within a local network (LAN). Not routable on the internet. These ranges are reusable in any private network.
  * **Private IPv4 Ranges:**
    * `10.0.0.0` to `10.255.255.255` (Class A)
    * `172.16.0.0` to `172.31.255.255` (Class B)
    * `192.168.0.0` to `192.168.255.255` (Class C)


### IPv4 vs. IPv6 Comparison (IMP)

IPv6 was developed to address the exhaustion of IPv4 addresses.


| Feature | IPv4 | IPv6 |
| :-- | :-- | :-- |
| **Address Size** | **32-bit** (approx. 4.3 billion addresses) | **128-bit** (approx. 340 undecillion addresses) |
| **Notation** | Dotted Decimal (e.g., `192.168.1.1`) | Hexadecimal with colons (e.g., `2001:0db8:85a3:0000:0000:8a2e:0370:7334`) |
| **Address Configuration** | Manual or via **DHCP**. | Can use **SLAAC** (Stateless Address Autoconfiguration), DHCPv6, or static. |
| **Security** | Optional (IPsec must be implemented separately). | **IPsec is built-in** and mandatory, providing better end-to-end security. |
| **Broadcasts** | Uses broadcast messages. | No broadcasts; uses **multicast** and **anycast** instead, which is more efficient. |

* **IPv6 Rule:** You can shorten IPv6 addresses by removing leading zeros in a block and replacing one consecutive series of zero blocks with `::`.
  * Example: `2001:0db8:0000:0000:AB00:0000:0000:0001` becomes `2001:db8::AB00:0:0:1` or `2001:db8:0:0:AB00::1`.
  * **Common Pitfall:** You can only use the double colon (`::`) once in an address.


### Subnetting, Supernetting, and Addressing

* **Classful Addressing (Legacy):** The original system where the IP address space was divided into classes (A, B, C, D, E). The class determined the default network/host portion. This system was inflexible and wasted many IP addresses.
* **Classless Addressing (CIDR - Classless Inter-Domain Routing):** The modern standard. It uses a **subnet mask** or a prefix (e.g., `/24`) to define the boundary between the network and host portions of an address. This allows for flexible and efficient allocation of IP addresses.
* **Subnetting (IMP):**
  * **What:** The process of dividing a single large network into multiple smaller, logical networks called **subnets**. This is done by "borrowing" bits from the host portion of the IP address to create subnet bits.
  * **Why:**
    * **Reduces Broadcast Traffic:** Broadcasts are contained within a subnet, improving network performance.
    * **Enhances Security:** You can apply different security policies to different subnets.
    * **Simplifies Management:** Smaller networks are easier to troubleshoot and manage.
  * **Analogy:** A city's postal system (a large network) uses ZIP codes (subnets) to divide the city. Mail delivery within a ZIP code is fast and efficient. Without ZIP codes, every mail carrier would have to know every single street in the entire city.

```
*   **Example:** You are given the network `192.168.1.0/24`. The `/24` means 24 bits for the network part and 8 for the host part. If you change the mask to `/26`, you've "borrowed" 2 bits for subnets. This creates 2<sup>2</sup> = 4 subnets, each with 2<sup>6</sup> - 2 = 62 usable host addresses.
```

* **Supernetting (Route Aggregation):**
  * **What:** The opposite of subnetting. It combines multiple smaller, contiguous network prefixes into a single, larger prefix.
  * **Why:** To reduce the size and complexity of routing tables on internet backbone routers.
  * **Example:** A router can advertise a single route for `200.20.0.0/22` instead of four separate routes for `200.20.0.0/24`, `200.20.1.0/24`, `200.20.2.0/24`, and `200.20.3.0/24`.


### Key Network Services (NAT, DHCP, DNS) (IMP)

| Protocol | Full Name | Purpose \& Function |
| :-- | :-- | :-- |
| **NAT** | **Network Address Translation** | Translates private IP addresses to a public IP address. Its primary function is to **conserve the limited supply of IPv4 addresses**. The most common form is **PAT (Port Address Translation)**, which uses port numbers to track unique internal connections, allowing many devices to share one public IP. |
| **DHCP** | **Dynamic Host Configuration Protocol** | **Automatically assigns IP addresses**, subnet masks, default gateways, and DNS server information to hosts on a network. This simplifies network administration. It uses a four-step process called **DORA** (Discover, Offer, Request, Acknowledgment). |
| **DNS** | **Domain Name System** | **Translates human-friendly domain names** (e.g., `www.perplexity.ai`) into machine-readable IP addresses. It functions as the "phonebook of the internet." When you type a URL, your computer performs a DNS query to find the correct IP address to connect to. |



</details>

---

<details>
  <summary>06: Routing and Switching</summary>

### Routing and Switching Fundamentals

* **Switching (Layer 2):** The process of using **MAC addresses** to forward data frames within a single local network (LAN). A switch creates a network; it connects devices together.
* **Routing (Layer 3):** The process of using **IP addresses** to move data packets between different networks. A router connects networks together.
* **Analogy:** Switching is like delivering mail within a single large office building (one network). The mail clerk knows everyone's desk location (MAC address). Routing is like the city's postal service deciding how to get a letter from one office building to another across town (between networks), using street addresses (IP addresses).


### Routing (IMP)

Routing is the process of selecting a path for traffic in a network or across multiple networks.

* **Static Routing:** Routes are manually configured by a network administrator.
  * **Pros:** Secure (no route advertisements), predictable, low CPU overhead.
  * **Cons:** Not scalable. If a link fails, the administrator must manually update the routes.
  * **Use Case:** Small, simple networks or for a specific, fixed route (like a default route).
* **Dynamic Routing:** Routers automatically learn about other networks from their neighbors using routing protocols.
  * **Pros:** Scalable, automatically adapts to network changes (topology changes).
  * **Cons:** Less secure (can be spoofed), requires more CPU/memory, can be complex.
  * **Use Case:** Most medium to large networks.


### Routing Algorithms (IMP)

Dynamic routing protocols use one of two main algorithms to determine the best path.


| Feature | Distance Vector | Link State |
| :-- | :-- | :-- |
| **Knowledge** | Knows only its directly connected neighbors ("Routing by rumor"). | Knows the entire network topology ("Everyone has a map"). |
| **Updates** | Sends its entire routing table periodically to neighbors. | Sends small updates (LSA - Link State Advertisements) only when a change occurs. |
| **Convergence** | Slower. A change must propagate hop-by-hop. | Faster. Updates are flooded to all routers at once. |
| **Resources** | Less CPU/memory intensive. | More CPU/memory intensive (due to SPF algorithm and topology database). |
| **Scalability** | Less scalable. Prone to **routing loops**. | Highly scalable. |
| **Protocols** | **RIP, IGRP** | **OSPF, IS-IS** |

* **Common Pitfall:** Routing loops in Distance Vector protocols. Mechanisms like **Split Horizon** (don't advertise a route back to the interface you learned it from) and **Poison Reverse** are used to prevent them.


### Routing Protocols (IMP)

| Protocol | Type | Metric | Standard | Key Characteristics |
| :-- | :-- | :-- | :-- | :-- |
| **RIP** | Distance Vector | Hop Count | Open | Simple but outdated. Max 15 hops. RIPv2 supports classless addressing (CIDR). |
| **EIGRP** | Advanced Distance Vector (Hybrid) | Bandwidth, Delay, Load, Reliability | Cisco Proprietary | Fast convergence using DUAL algorithm. More efficient than traditional Distance Vector. |
| **OSPF** | Link State | Cost (based on bandwidth) | Open | Very popular IGP. Scalable, stable, and widely used in enterprise networks. Uses Dijkstra's algorithm. |
| **BGP** | Path Vector | Policy-based attributes (AS-Path, etc.) | Open | The protocol of the **Internet**. It is an **Exterior Gateway Protocol (EGP)** used to exchange routing information **between** Autonomous Systems (AS). Unlike IGPs, it doesn't care about speed, but about policy. |

* **IGP vs. EGP (IMP):**
  * **IGP (Interior Gateway Protocol):** Used for routing *within* an Autonomous System (e.g., OSPF, EIGRP). The goal is to find the fastest path.
  * **EGP (Exterior Gateway Protocol):** Used for routing *between* Autonomous Systems (e.g., BGP). The goal is to enforce policy.

**Real-World Example: A Simple Routing Table**

```
# Command: route -n (Linux) or netstat -r (Windows/macOS)

Kernel IP routing table
Destination     Gateway         Genmask         Flags   Metric  Ref    Use Iface
0.0.0.0         192.168.1.1     0.0.0.0         UG      100     0        0 wlan0
10.8.0.0        0.0.0.0         255.255.255.0   U       0       0        0 tun0
192.168.1.0     0.0.0.0         255.255.255.0   U       100     0        0 wlan0
```

* The first line is the **default route**: any traffic not destined for the other networks (`0.0.0.0`) is sent to the gateway `192.168.1.1` (your home router).
* The third line is the **local network**: traffic for `192.168.1.x` is sent directly out on the `wlan0` interface.


### Switching Techniques

This refers to how a switch forwards an Ethernet frame from an input port to an output port.

* **Store-and-Forward:**
  * The switch receives the **entire frame** and stores it in a buffer.
  * It performs an error check using the **FCS (Frame Check Sequence)**.
  * If the frame is error-free, it is forwarded. If not, it is discarded.
  * **Pros:** Highest accuracy. **Cons:** Higher latency.
  * **Best Practice:** This is the most common method used in modern switches.
* **Cut-Through:**
  * The switch reads only the **destination MAC address** of the frame and immediately begins forwarding it to the appropriate port.
  * It does *not* wait for the rest of the frame to arrive.
  * **Pros:** Lowest latency. **Cons:** Forwards error-filled frames (runts) and collision fragments, as it doesn't check the FCS.


</details>

---

<details>
  <summary>07: Network Technologies & Standards</summary>

### Ethernet Standards (IEEE 802.3)

**IEEE 802.3** is the standard that defines wired LAN communication (Ethernet). It specifies the physical layer (cabling) and the MAC sublayer of the data link layer.


| Standard Name | Common Name | Speed | Typical Cable |
| :-- | :-- | :-- | :-- |
| **802.3u** | Fast Ethernet | 100 Mbps | Cat5, Cat5e |
| **802.3z** | Gigabit Ethernet | 1 Gbps | Cat5e, Cat6, Fiber |
| **802.3an** | 10GBASE-T | 10 Gbps | Cat6a, Cat7 |
| **802.3ae** | 10 Gigabit Ethernet | 10 Gbps | Fiber Optic |

### Wireless Networking (IEEE 802.11)

**IEEE 802.11** is the set of standards for implementing Wireless Local Area Networks (WLAN), commonly known as **Wi-Fi**.


| Standard | Wi-Fi Name | Frequency Band(s) | Max Theoretical Speed | Key Feature |
| :-- | :-- | :-- | :-- | :-- |
| **802.11g** | Wi-Fi 3 | 2.4 GHz | 54 Mbps | Backward compatible with 802.11b. |
| **802.11n** | Wi-Fi 4 | 2.4 / 5 GHz | ~600 Mbps | Introduced **MIMO** (Multiple Input, Multiple Output) for better throughput. |
| **802.11ac** | **Wi-Fi 5 (IMP)** | 5 GHz only | ~1.3 Gbps+ | Wider channels, more MIMO streams. Most common standard in use today. |
| **802.11ax** | **Wi-Fi 6 (IMP)** | 2.4 / 5 GHz | ~10 Gbps+ | Focuses on efficiency in crowded environments using **OFDMA**. |

* **Best Practice:** Be familiar with the new Wi-Fi naming convention (Wi-Fi 5, Wi-Fi 6), as it simplifies the standards.


### VLANs (Virtual LANs) (IMP)

A **VLAN** is a logical grouping of devices on one or more physical LANs that are configured to communicate as if they were attached to the same wire, when in fact they are located on a number of different LAN segments.

* **What it does:** A VLAN logically segments a single physical switch into multiple, separate broadcast domains.
* **Analogy:** Think of a large office building as a single physical switch. A VLAN is like creating virtual "departments" (e.g., VLAN 10 for Sales, VLAN 20 for Engineering). People in Sales can only talk to each other, and people in Engineering can only talk to each other, even if their desks (and switch ports) are side-by-side.
* **Benefits:**
  * **Security:** Isolates traffic between groups.
  * **Performance:** Reduces broadcast traffic, as broadcasts are confined to their own VLAN.
  * **Flexibility:** Group users by department or function, regardless of their physical location.
* **Inter-VLAN Routing (IMP):** For a device in one VLAN (e.g., Sales) to communicate with a device in another VLAN (e.g., Engineering), a **Layer 3 device (a router or a Layer 3 switch)** is required. This process is called **inter-VLAN routing**. A common configuration is called "Router-on-a-Stick," where a single router interface handles traffic for multiple VLANs.


### Spanning Tree Protocol (STP - IEEE 802.1D) (IMP)

STP is a Layer 2 network protocol that ensures a loop-free topology for any bridged Ethernet network.

* **Problem:** Redundant links between switches are great for fault tolerance, but they create **switching loops**. A broadcast frame can get caught in a loop, endlessly circling the network, creating a **broadcast storm** that consumes all available bandwidth and brings the network down.
* **Solution:** STP prevents these loops by logically blocking redundant paths.
* **How it works:**

1. **Elect a Root Bridge:** Switches elect a single "master" switch called the Root Bridge.
2. **Find Best Paths:** Each non-root switch determines its single best path to the Root Bridge. This port becomes the **Root Port**.
3. **Block Redundant Paths:** Any other paths that could create a loop are put into a **`Blocking` state**. These ports don't forward data but listen for changes.
4. **Failover:** If the primary path fails, STP automatically unblocks a blocked port to restore connectivity.
* **Protocol Version Notes:**
  * **STP (802.1D):** The original, very slow to converge (30-50 seconds).
  * **RSTP (Rapid Spanning Tree Protocol - 802.1w):** A significant improvement, converging in seconds. This is the de facto standard today.
  * **PVST+/RPVST+:** Cisco proprietary versions that run a separate STP instance per VLAN.


</details>

---

<details>
  <summary>08: Network Security</summary>

### Network Security Fundamentals

The core goal of network security is to protect the **CIA Triad**:

* **Confidentiality:** Ensuring that data is accessible only to authorized users. (Achieved via **Encryption**).
* **Integrity:** Ensuring that data has not been altered or tampered with in transit. (Achieved via **Hashing**).
* **Availability:** Ensuring that network services and data are available to authorized users when needed. (Protected by firewalls, IDS/IPS, and redundant designs).


### Firewall and their Types (IMP)

A **firewall** is a network security device that monitors incoming and outgoing network traffic and decides whether to allow or block specific traffic based on a defined set of security rules.

* **Analogy:** A firewall is like a security guard at the entrance of a building. It checks the ID (IP address, port number) of everyone trying to enter and decides whether to let them in based on a pre-approved list.

| Firewall Type | OSI Layer | How it Works | Pros / Cons |
| :-- | :-- | :-- | :-- |
| **Packet-Filtering** | Layer 3/4 (Network/Transport) | Examines the header of each packet (IP address, port number) in isolation. Stateless. | **Pros:** Fast, simple. **Cons:** Not very secure, doesn't understand context. Can be tricked by spoofed IP addresses. |
| **Stateful Inspection** | Layer 3/4 (Network/Transport) | Keeps track of the state of network connections (e.g., TCP streams). It knows if a packet is part of an established, legitimate conversation. | **Pros:** More secure than packet filtering, offers good performance. **Cons:** Can be vulnerable to complex Layer 7 attacks. |
| **Proxy (Application Gateway)** | Layer 7 (Application) | Acts as an intermediary between the user and the internet. It makes requests on behalf of the user. | **Pros:** High security, can inspect the actual content of the traffic (deep packet inspection). **Cons:** Can create a performance bottleneck. |
| **Next-Generation (NGFW)** | Layers 3-7 | Combines stateful inspection with application-level awareness, deep packet inspection (DPI), and integrated IDS/IPS. | **Pros:** All-in-one security solution, highly aware of modern threats. **Cons:** Complex, can be expensive. |

### Intrusion Detection and Prevention Systems (IDS/IPS) (IMP)

* **IDS (Intrusion Detection System):** A passive device that monitors network traffic for suspicious activity, logs it, and sends an alert. It **detects** but does not stop the attack.
  * **Analogy:** A security camera system that records suspicious activity and alerts a guard.
* **IPS (Intrusion Prevention System):** An active device that sits in-line with traffic. It monitors, detects, and **actively blocks** malicious traffic before it reaches the target.
  * **Analogy:** A security guard at the door who can physically stop an unauthorized person from entering.

**Detection Methods:**

* **Signature-based:** Looks for known patterns (signatures) of malicious traffic. Good against known attacks but cannot detect new "zero-day" attacks.
* **Anomaly-based:** Establishes a baseline of normal network behavior and alerts on any deviation from that baseline. Can detect new attacks but may generate false positives.


### Virtual Private Networks (VPNs) (IMP)

A **VPN** extends a private network across a public network (like the internet), enabling users to send and receive data as if their devices were directly connected to the private network. It creates a secure, encrypted **tunnel**.

* **Analogy:** A VPN is like an armored truck driving on a public highway. Anyone can see the truck (the encrypted packet), but no one can see what's inside (the actual data).
* **Common Protocols:**
  * **IPsec (Internet Protocol Security):** A suite of protocols that provides security at the Network Layer (Layer 3). It's often used for site-to-site VPNs (connecting two office networks).
  * **SSL/TLS (Secure Sockets Layer/Transport Layer Security):** Operates at the Application Layer. It's commonly used for remote access VPNs (a single user connecting to a corporate network), often right from a web browser.
* **Public Key Infrastructure (PKI):** PKI is the framework of hardware, software, and policies used to manage digital certificates and public-key encryption. VPNs and other secure systems use digital certificates (issued by a Certificate Authority) to verify the identity of the communicating parties before establishing a secure tunnel.


### Cryptography Basics (IMP)

| Type | Symmetric Encryption | Asymmetric Encryption |
| :-- | :-- | :-- |
| **Keys** | Uses a **single, shared secret key** for both encryption and decryption. | Uses a **key pair**: a public key (to encrypt) and a private key (to decrypt). |
| **Speed** | **Fast.** Less computationally intensive. | **Slow.** More computationally intensive. |
| **Key Management** | Difficult. Securely sharing the secret key is a major challenge. | Easy. The public key can be shared freely. |
| **Algorithms** | AES, DES, 3DES | RSA, ECC |
| **Use Case** | Encrypting bulk data in a session. | Securely exchanging the symmetric key at the beginning of a session; digital signatures. |

* **Best Practice - Hybrid Encryption:** In practice (like with HTTPS/TLS), both are used. Asymmetric encryption is used first to securely share a randomly generated symmetric key. Then, that fast symmetric key is used to encrypt the rest of the conversation. This provides the best of both worlds.


</details>

---

<details>
  <summary>09: Network Management & Monitoring</summary>

### Traffic Management Techniques

Traffic management involves controlling network traffic to optimize performance, improve security, and increase reliability. Key techniques include:

* **Traffic Shaping (Policing):** The process of delaying some or all datagrams to bring them into compliance with a desired traffic profile. It "smooths out" traffic bursts to prevent congestion.
  * **Analogy:** A traffic light on a highway on-ramp that controls the rate at which cars can merge, preventing jams on the highway itself.
* **Load Balancing:** Distributing network traffic across multiple servers to ensure no single server becomes a bottleneck. (Covered more in Section 10).
* **Quality of Service (QoS):** A set of techniques used to manage network resources and prioritize traffic.


### Quality of Service (QoS), Bandwidth, and Latency (IMP)

This is a critical area for understanding network performance.

* **Quality of Service (QoS):**
  * **What:** The ability to provide different priority levels to different applications, users, or data flows.
  * **Why:** Not all traffic is equal. Real-time traffic like **VoIP** or **video conferencing** is very sensitive to delay and jitter, while traffic like **email** or **file transfers** is not. QoS ensures that high-priority applications get the network resources they need.
  * **Analogy:** QoS creates an "HOV lane" on the network highway. Ambulances and buses (VoIP/video) get to use the priority lane, while regular cars (email/web browsing) stay in the standard lanes.
* **Bandwidth and Latency:**
  * **Bandwidth:** The maximum rate at which data can be transferred over a network path. Measured in bits per second (bps). It represents the **capacity** of the link.
  * **Latency:** The time it takes for a single bit of data to travel from the source to the destination. Measured in milliseconds (ms). It represents **delay**.
  * **Analogy (IMP):** Think of a highway.
    * **Bandwidth** is the number of lanes on the highway. A 10-lane highway has more bandwidth than a 2-lane road.
    * **Latency** is the speed limit of the highway. It's the time it takes for one car to get from Point A to Point B, regardless of how many lanes there are.
* **Network Congestion and Control:**
  * **Congestion:** Occurs when a network link or node is carrying so much data that its quality of service deteriorates. Symptoms include high latency, jitter, and packet loss.
  * **TCP Congestion Control:** TCP has built-in mechanisms to handle congestion, including:
    * **Slow Start:** Begins by sending a small number of segments and exponentially increases the amount of data sent until packet loss is detected.
    * **Congestion Avoidance:** Once a certain threshold is reached, TCP slows its growth rate to avoid causing congestion.


### Network Performance Metrics

These are key indicators used to measure the performance of a network.

* **Throughput:** The actual rate of successful data transfer (as opposed to bandwidth, which is the theoretical maximum).
* **Jitter:** The variation in the delay of received packets. High jitter is very disruptive for VoIP and video streaming.
* **Packet Loss:** The percentage of packets that are lost in transit and fail to reach their destination.
* **Error Rate:** The percentage of transmitted bits that are corrupted during transmission.


### Network Troubleshooting Techniques (IMP)

A systematic approach is key. A common interview question is "How would you troubleshoot a user who can't connect to the internet?"

**Methodology:** Follow the OSI model, either top-down or bottom-up.

* **Bottom-Up:** Start at Layer 1 and work your way up. Is the cable plugged in? Are the lights on the switch port on?
* **Top-Down:** Start at Layer 7 and work down. Can the user access any application? Can they resolve a DNS name?

**Common Troubleshooting Tools:**


| Command | Function | Example |
| :-- | :-- | :-- |
| `ping` | Checks Layer 3 connectivity to a host and measures latency. | `ping 8.8.8.8` |
| `traceroute` / `tracert` | Shows the hop-by-hop path packets take to a destination. | `traceroute google.com` |
| `ipconfig` / `ifconfig` | Displays the IP configuration of a host (IP, subnet mask, gateway). | `ipconfig /all` |
| `nslookup` / `dig` | Queries DNS servers to resolve domain names to IP addresses. | `nslookup perplexity.ai` |

### Network Protocol Analysis Tools (Wireshark, tcpdump) (IMP)

These tools capture and display the data traveling over a network.

* **Wireshark:**
  * **What:** The world's most popular graphical network protocol analyzer.
  * **Features:** Provides deep inspection of hundreds of protocols, with powerful filtering and color-coding to visualize traffic.
  * **Use Case:** Ideal for detailed, visual analysis of network problems on a desktop. You can easily see the TCP three-way handshake, HTTP requests, DNS queries, etc.
  * **Real-World Example:** A developer can use Wireshark to see if their application is sending correctly formatted API requests and to inspect the server's response.
* **tcpdump:**
  * **What:** A powerful command-line packet analyzer.
  * **Features:** Lightweight and available on virtually all Unix-like operating systems. Excellent for capturing traffic on remote servers or network devices where a GUI is not available.
  * **Use Case:** Running a long-term capture on a remote server, scripting captures, or quickly checking traffic without the overhead of a GUI.
  * **Short Command Example:** `tcpdump -i eth0 host 192.168.1.50 and port 443`
    * This command captures traffic on the `eth0` interface that is going to or from the IP address `192.168.1.50` on port `443` (HTTPS).


</details>

---

<details>
  <summary>10: Advanced Networking Concepts</summary>

### Client-Server vs. Peer-to-Peer (P2P) Architectures

| Feature | Client-Server Model | Peer-to-Peer (P2P) Model |
| :-- | :-- | :-- |
| **Architecture** | A centralized server provides resources and services to multiple clients. | All nodes (peers) are equal; they can act as both a client and a server. |
| **Data Storage** | Centralized on the server. | Distributed across all peers. |
| **Scalability** | Can become a bottleneck as the number of clients increases. Scaling often requires upgrading the central server (vertical scaling). | Highly scalable. As more peers join, the total capacity of the network increases. |
| **Reliability** | A single point of failure. If the server goes down, the entire service is unavailable. | Highly resilient. If one peer goes down, the network continues to function. |
| **Examples** | Web browsing (you are the client, the website's server is the server), email. | BitTorrent, Skype (in its early days), cryptocurrencies like Bitcoin. |

### Network Design Principles and Considerations

Good network design is built on a hierarchical model, typically with three layers:

* **Access Layer:** Where end-user devices (PCs, phones) connect to the network. Primary function is to provide network access.
* **Distribution Layer:** Aggregates traffic from the access layer and acts as the boundary between the access and core layers. This is where policies (like routing, filtering, QoS) are often applied.
* **Core Layer:** The high-speed backbone of the network. Its only job is to switch traffic as fast as possible. It should be highly reliable and redundant.

**Key Considerations:**

* **Redundancy \& Fault Tolerance:** Designing the network so that no single point of failure can take it down. This involves redundant links, redundant devices (e.g., two core routers), and protocols like STP and HSRP/VRRP (for first-hop redundancy).
* **Scalability:** The ability of the network to grow without major redesign.
* **Security:** Integrating security at every layer of the network (Defense in Depth).


### Load Balancing Techniques (IMP)

Load balancing is the process of distributing traffic efficiently across a group of backend servers (a "server farm" or "pool").

* **Analogy:** A load balancer is like a traffic cop at a toll plaza, directing cars to the shortest available toll booth lane to prevent any single booth from getting backed up.

**Common Algorithms:**

* **Round Robin:** Sequentially sends each new request to the next server in the pool. Simple but doesn't account for server load.
* **Least Connections:** Sends each new request to the server that currently has the fewest active connections. More intelligent than Round Robin.
* **IP Hash:** The client's IP address is used to determine which server receives the request. This ensures that a user will consistently connect to the same server (useful for maintaining session state).


### Content Delivery Networks (CDNs)

A **CDN** is a geographically distributed network of proxy servers and their data centers.

* **Goal:** To provide high availability and performance by distributing the service spatially relative to end-users.
* **How it works:** When you request content (like an image or video) from a website that uses a CDN, the request is redirected to a CDN server that is geographically closest to you. This reduces latency and offloads traffic from the origin server.
* **Example:** When a user in India streams a Netflix show, they are likely streaming it from a Netflix CDN server located in India, not from a central server in the US.


### Network Virtualization

Network virtualization is the process of combining hardware and software network resources and network functionality into a single, software-based administrative entity called a virtual network.

* **Example:** **VLANs** are a simple form of network virtualization. A more advanced example is **VXLAN (Virtual Extensible LAN)**, which allows you to stretch a Layer 2 network over a Layer 3 infrastructure, a key technology in modern data centers.


### Software-Defined Networking (SDN) (IMP)

SDN is a network architecture approach that enables the network to be intelligently and centrally controlled, or "programmed," using software applications.

* **Key Concept:** SDN decouples the **Control Plane** (which decides where traffic should go) from the **Data Plane** (which actually forwards the traffic).
* **Traditional Networking:** In a traditional router or switch, the control plane and data plane are tightly integrated on the device itself. Each device makes its own decisions.
* **SDN:** The control plane is moved to a centralized **SDN Controller**. The controller has a global view of the entire network and can push down forwarding rules to the (now much simpler) switches and routers.
* **Analogy:**
  * **Traditional:** A convoy of cars where each driver decides their own route.
  * **SDN:** A centrally-managed fleet of self-driving cars where a central computer calculates the optimal route for every car and sends them instructions.


### Network Reliability and Fault Tolerance

This involves strategies to keep the network operational despite failures.

* **Link Aggregation (EtherChannel):** Bundling multiple physical links into a single logical link to increase bandwidth and provide redundancy. If one physical link in the bundle fails, traffic is automatically redistributed over the remaining links.
* **First-Hop Redundancy Protocols (FHRP):**
  * **Problem:** If a host's default gateway router fails, it loses all connectivity outside its local network.
  * **Solution:** Protocols like **HSRP (Hot Standby Router Protocol)** and **VRRP (Virtual Router Redundancy Protocol)** allow two or more routers to share a single virtual IP address and act as a single virtual router. One router is "active," and the other is on "standby." If the active router fails, the standby router takes over seamlessly.


</details>