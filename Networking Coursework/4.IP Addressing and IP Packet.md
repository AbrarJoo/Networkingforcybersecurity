# IP Addressing and IP Packet

# ***IP Addressing and IP Packets – Detailed Notes***

---

## 1️⃣ IP Address Classes

### Overview

- IP addresses are **32-bit logical identifiers** for devices on a network.
- IPv4 addresses are traditionally divided into **classes A, B, C, D, E** for organization.

### Classes

| Class | Range (First Octet) | Default Network Mask | Usage |
| --- | --- | --- | --- |
| A | 0–127 | 255.0.0.0 (/8) | Large networks, few networks, many hosts |
| B | 128–191 | 255.255.0.0 (/16) | Medium networks |
| C | 192–223 | 255.255.255.0 (/24) | Small networks, many networks, few hosts |
| D | 224–239 | N/A | Multicast |
| E | 240–255 | N/A | Experimental / Reserved |

### 1.1 Local Host IP

- **127.0.0.1** → loopback address, refers to the local host.
- Used for testing network applications locally.

### 1.2 Private vs Public IP Addresses

- **Private IPs:** Used inside LANs, not routable on the Internet
- **Public IPs:** Globally unique, routable on the Internet

| Private Class | Private Range | Default Network Mask |
| --- | --- | --- |
| A | 10.0.0.0 – 10.255.255.255 | 255.0.0.0 (/8) |
| B | 172.16.0.0 – 172.31.255.255 | 255.255.0.0 (/16) |
| C | 192.168.0.0 – 192.168.255.255 | 255.255.255.0 (/24) |

### 1.3 NAT Technology

- **Network Address Translation** converts private IP addresses to public IP addresses.
- Enables multiple devices to share **one public IP**.
- Types: Static NAT, Dynamic NAT, PAT (Port Address Translation)

### 1.4 Definition of a Network (IP Based)

- A network is a **group of devices sharing the same network prefix**.
- **Network prefix** identifies the network portion of an IP address.
- **Network mask / subnet mask** separates network and host portions.

---

## 2️⃣ Public IP Addresses

### Public IP Ranges (RIPE / IANA allocations)

| Class | Range | Notes |
| --- | --- | --- |
| A | 1.0.0.0 – 126.255.255.255 | Large public networks |
| B | 128.0.0.0 – 191.255.255.255 | Medium networks |
| C | 192.0.0.0 – 223.255.255.255 | Small networks |
- Managed by **RIRs (e.g., RIPE, ARIN, APNIC)** for global allocation

### Static vs Dynamic IP Addresses

| Type | Description | Advantages | Disadvantages |
| --- | --- | --- | --- |
| Static | Manually assigned, permanent | Reliable for servers, easy remote access | Management overhead, inflexible |
| Dynamic | Assigned by DHCP | Easy management, flexible, reduces IP conflicts | IP can change, not suitable for permanent services |

### Other IP Related Services

- **DDNS (Dynamic DNS):** Maps changing IP addresses to a fixed hostname
- **DHCP (Dynamic Host Configuration Protocol):** Automatically assigns IP addresses to devices in a network

---

## 3️⃣ Summary / Key Points

- IP addresses are **32-bit logical identifiers** used to communicate across networks
- Classes A, B, C are for **unicast**, D for multicast, E reserved
- **Localhost 127.0.0.1** for self-reference
- **Private IP ranges**: A (10.x.x.x), B (172.16–31.x.x), C (192.168.x.x)
- **Public IPs**: Globally unique, managed by RIPE/IANA
- **NAT** allows private IPs to communicate over the Internet
- Static IP → permanent; Dynamic IP → assigned by DHCP
- **DDNS** keeps hostname mapping updated with changing IPs

---

# ***IPv4 Packet Structure and Wireshark Analysis***

![Screenshot 2026-01-05 112151.png](Screenshot_2026-01-05_112151.png)

---

## 1️⃣ Introduction to IPv4 Packets

- IPv4 operates at **OSI Layer 3 (Network Layer)**.
- Data from the transport layer is encapsulated into an **IP packet (datagram)**.
- The IPv4 header contains **routing, fragmentation, and delivery information**.

Minimum IPv4 header size: **20 bytes**

Maximum IPv4 header size: **60 bytes** (with options)

---

## 2️⃣ IPv4 Header Structure (Field-by-Field Deep Dive)

### 2.1 Version

- **Size:** 4 bits
- Indicates IP version
- Value for IPv4 = **4**
- Used by devices to interpret the packet format

---

### 2.2 IHL (Internet Header Length)

- **Size:** 4 bits
- Specifies the **header length** in 32-bit words
- Minimum value: **5** (5 × 4 = 20 bytes)
- Increases when **options** are present

---

### 2.3 DSCP (Differentiated Services Code Point)

- **Size:** 6 bits (part of former ToS field)
- Used for **Quality of Service (QoS)**
- Prioritizes traffic (voice, video, data)

---

### 2.4 ECN (Explicit Congestion Notification)

- **Size:** 2 bits
- Used to indicate **network congestion** without dropping packets
- Helps reduce packet loss

---

### 2.5 Total Length

- **Size:** 16 bits
- Indicates total size of IP packet (header + data)
- Maximum size: **65,535 bytes**

---

### 2.6 Identification

- **Size:** 16 bits
- Used to **reassemble fragmented packets**
- All fragments of a packet share the same ID

---

### 2.7 Flags

- **Size:** 3 bits

| Bit | Meaning |
| --- | --- |
| Reserved | Always 0 |
| DF | Don’t Fragment |
| MF | More Fragments |
- DF = prevents fragmentation
- MF = indicates more fragments follow

---

### 2.8 Fragment Offset

- **Size:** 13 bits
- Indicates position of fragment in original packet
- Measured in **8-byte blocks**

---

### 2.9 Time To Live (TTL)

- **Size:** 8 bits
- Prevents infinite routing loops
- Decremented by **1 at each router**
- Packet discarded when TTL reaches 0

---

### 2.10 Protocol

- **Size:** 8 bits
- Identifies the **encapsulated transport protocol**

| Value | Protocol |
| --- | --- |
| 1 | ICMP |
| 6 | TCP |
| 17 | UDP |

---

### 2.11 Header Checksum

- **Size:** 16 bits
- Error detection for **IP header only**
- Recalculated at every router due to TTL change

---

### 2.12 Source IP Address

- **Size:** 32 bits
- IP address of the sending host

---

### 2.13 Destination IP Address

- **Size:** 32 bits
- IP address of the receiving host

---

### 2.14 Options (Optional)

- Variable length (0–40 bytes)
- Rarely used
- Examples: security, record route, timestamp

---

### 2.15 Data (Payload)

- Contains **transport-layer segment** (TCP/UDP)
- Size depends on MTU and header length

---

## 3️⃣ IPv4 Packet Encapsulation Summary

```
[ Ethernet Header ]
[ IPv4 Header ]
[ TCP / UDP Header ]
[ Application Data ]

```

- IP provides **best-effort delivery**
- No guarantee of delivery, order, or duplication

---

## 4️⃣ Analyzing IPv4 Packet Using Wireshark

![Screenshot 2026-01-05 113542.png](Screenshot_2026-01-05_113542.png)

### 4.1 Locating IPv4 Header in Wireshark

- Capture traffic and select a packet
- Expand:
    - Ethernet II
    - Internet Protocol Version 4

---

### 4.2 Field Observation in Wireshark

- **Version:** Shows IPv4
- **Header Length:** Displayed in bytes
- **DSCP / ECN:** Shown under Differentiated Services Field
- **Total Length:** Packet size
- **Identification:** Useful for fragmentation analysis
- **Flags:** DF/MF bits visible
- **Fragment Offset:** Usually 0 (no fragmentation)
- **TTL:** Default values (64, 128, 255)
- **Protocol:** TCP / UDP / ICMP
- **Header Checksum:** Marked “Good” or “Bad”
- **Source & Destination IPs:** Clearly visible
- **Options:** Rarely present

---

### 4.3 Practical Observations

- TTL helps identify **operating systems**
- Protocol field determines next-layer decoding
- Fragmentation is rare in modern networks
- Header checksum errors indicate corruption

---

## 5️⃣ Cybersecurity Relevance

- TTL manipulation → OS fingerprinting
- Fragmentation → evasion techniques
- Protocol field → traffic classification
- IP spoofing → fake source IP addresses

---

## ✅ Summary

- IPv4 header = **routing + control information**
- Minimum header size = 20 bytes
- Fragmentation handled using ID, flags, offset
- TTL prevents routing loops
- Wireshark exposes all IPv4 header fields
- Understanding IP packets is critical for:
    - Packet analysis
    - Firewall rules
    - Intrusion detection
    - Web security & bug bounty

---