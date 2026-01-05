# physical & data link layer

## ***1. Bits and Bytes***

### Bit

- A **bit (binary digit)** is the smallest unit of data in computing.
- It can have only **two values: 0 or 1**.
- Used to represent digital signals (on/off, true/false).

### Byte

- A **byte = 8 bits**.
- A byte can represent **256 different values (0–255)**.
- Commonly used to represent:
    - Characters (ASCII)
    - Small numbers
    - Basic data units in memory

### Units of Data

- 1 Byte (B) = 8 bits
- 1 Kilobyte (KB) = 1024 Bytes
- 1 Megabyte (MB) = 1024 KB
- 1 Gigabyte (GB) = 1024 MB

### Importance in Networking

- Network speeds are measured in **bits per second (bps)**.
- File sizes are measured in **bytes**.
- Understanding this difference is critical when analyzing traffic and bandwidth.

---

## 2. OSI Model (Open Systems Interconnection Model)

### Overview

- Developed by **ISO**.
- Conceptual model with **7 layers**.
- Used for **learning, troubleshooting, and standardization**.

### OSI Layers (Top to Bottom)

### Layer 7 – Application

- Interface between **user applications and the network**.
- Examples:
    - HTTP, HTTPS
    - FTP
    - SMTP, POP3
    - DNS

### Layer 6 – Presentation

- Responsible for **formatting and encryption**.
- Functions:
    - Data encoding/decoding
    - Compression
    - Encryption/Decryption (SSL/TLS)

### Layer 5 – Session

- Manages **sessions between devices**.
- Functions:
    - Session establishment
    - Session maintenance
    - Session termination

### Layer 4 – Transport

- Provides **end-to-end communication**.
- Handles:
    - Segmentation
    - Flow control
    - Error control
- Protocols:
    - TCP (reliable)
    - UDP (fast, unreliable)

### Layer 3 – Network

- Responsible for **logical addressing and routing**.
- Functions:
    - IP addressing
    - Packet forwarding
- Devices:
    - Routers
- Protocols:
    - IP, ICMP

### Layer 2 – Data Link

- Responsible for **node-to-node delivery**.
- Functions:
    - MAC addressing
    - Framing
    - Error detection
- Devices:
    - Switches
- Protocols:
    - Ethernet
    - ARP

### Layer 1 – Physical

- Deals with **physical transmission of data**.
- Includes:
    - Cables
    - Voltage levels
    - Bits on the wire
- Devices:
    - Hubs
    - Cables

---

## 3. TCP/IP Model

### Overview

- Developed by **DARPA**.
- Practical model used in the **real internet**.
- Consists of **4 layers**.

### TCP/IP Layers

### Application Layer

- Combines OSI layers **7, 6, and 5**.
- Protocols:
    - HTTP/HTTPS
    - FTP
    - SMTP
    - DNS

### Transport Layer

- Same as OSI Layer 4.
- Protocols:
    - TCP
    - UDP

### Internet Layer

- Same as OSI Layer 3.
- Protocols:
    - IP
    - ICMP

### Network Access Layer

- Combines OSI layers **2 and 1**.
- Handles:
    - Framing
    - MAC addressing
    - Physical transmission

---

## 4. Protocol Data Units (PDUs)

### Definition

- A **PDU** is the unit of data passed between layers in a network model.

### PDUs by OSI Layer

- Layer 7–5: **Data**
- Layer 4: **Segment (TCP) / Datagram (UDP)**
- Layer 3: **Packet**
- Layer 2: **Frame**
- Layer 1: **Bits**

### Importance

- Helps in understanding **encapsulation and decapsulation**.
- Used in **Wireshark analysis** and troubleshooting.

---

## 5. Encapsulation Process

- Data is created at the Application layer.
- Each lower layer adds its **own header**.
- Final transmission occurs as **bits** on the physical medium.

Decapsulation happens in reverse order at the receiver.

---

## 6. Comparison: OSI Model vs TCP/IP Model

| Feature | OSI Model | TCP/IP Model |
| --- | --- | --- |
| Layers | 7 | 4 |
| Developed by | ISO | DARPA |
| Nature | Theoretical | Practical |
| Usage | Learning & troubleshooting | Real-world networking |
| Layer separation | Very strict | Less strict |

### Layer Mapping

- OSI 7,6,5 → TCP/IP Application
- OSI 4 → TCP/IP Transport
- OSI 3 → TCP/IP Internet
- OSI 2,1 → TCP/IP Network Access

---

## 7. Wireshark and Its Relevance

### What is Wireshark?

- A **network packet analyzer**.
- Captures and inspects network traffic in real time.

### Relevance to OSI & TCP/IP

- Displays traffic based on **protocol layers**.
- Helps visualize:
    - PDUs
    - Headers
    - Encapsulation

### Cybersecurity Importance

- Detects:
    - Suspicious traffic
    - Packet flooding
    - Unencrypted data leaks
- Used for:
    - Incident response
    - Malware traffic analysis
    - Network troubleshooting

---

## 8. Exam & Cybersecurity Key Points

- OSI is **conceptual**, TCP/IP is **practical**.
- TCP provides **reliability**, UDP provides **speed**.
- Wireshark works mainly at **Layers 2–7**.
- Understanding PDUs is essential for **packet analysis**.
- Most cyber attacks exploit **Application and Transport layers**.

## ***Encapsulation and Decapsulation***

![Screenshot 2026-01-01 213205.png](Screenshot_2026-01-01_213205.png)

### Encapsulation

### Definition

- **Encapsulation** is the process of wrapping data with protocol-specific information as it moves **down the network layers** from sender to receiver.
- Each layer adds its own **header** (and sometimes trailer) before passing data to the next lower layer.

### Why Encapsulation is Needed

- To ensure **correct delivery** of data
- To provide **addressing information** (IP, MAC, ports)
- To enable **error detection and control**
- To allow devices to understand **how to process received data**

### Encapsulation Process (OSI Model Perspective)

1. **Application Layer (Layer 7)**
    - User data is created (e.g., HTTP request, email).
    - PDU: **Data**
2. **Presentation Layer (Layer 6)**
    - Data may be **compressed or encrypted**.
    - PDU: **Data**
3. **Session Layer (Layer 5)**
    - Session information is added.
    - PDU: **Data**
4. **Transport Layer (Layer 4)**
    - Data is broken into smaller pieces.
    - Adds:
        - Source and destination **port numbers**
        - Sequence numbers (TCP)
    - PDU:
        - **Segment** (TCP)
        - **Datagram** (UDP)
5. **Network Layer (Layer 3)**
    - Adds:
        - Source and destination **IP addresses**
    - Determines best path to destination.
    - PDU: **Packet**
6. **Data Link Layer (Layer 2)**
    - Adds:
        - Source and destination **MAC addresses**
        - Error-checking trailer (FCS)
    - PDU: **Frame**
7. **Physical Layer (Layer 1)**
    - Frame is converted into **bits (0s and 1s)**.
    - Data is transmitted over the physical medium.

---

### Decapsulation

### Definition

- **Decapsulation** is the reverse process of encapsulation.
- Occurs at the **receiving device**, where headers and trailers are removed layer by layer.

### Decapsulation Process

1. **Physical Layer**
    - Receives raw bits from the medium.
2. **Data Link Layer**
    - Converts bits into frames.
    - Checks MAC address and error detection.
    - Removes Layer 2 header and trailer.
3. **Network Layer**
    - Examines destination IP address.
    - Removes IP header.
4. **Transport Layer**
    - Uses port numbers to deliver data to correct application.
    - Reassembles segments (TCP).
    - Removes transport header.
5. **Session, Presentation, Application Layers**
    - Decrypts and decompresses data if required.
    - Delivers original data to the application.

---

### Encapsulation vs Decapsulation (Quick Comparison)

| Encapsulation | Decapsulation |
| --- | --- |
| Sender side | Receiver side |
| Adds headers | Removes headers |
| Top to bottom (Layer 7 → 1) | Bottom to top (Layer 1 → 7) |
| Prepares data for transmission | Extracts usable data |

---

### Relevance to Cybersecurity

- Attackers often target specific **layers during encapsulation**:
    - Layer 7: Application attacks (SQL injection, XSS)
    - Layer 4: Port scanning, SYN floods
    - Layer 3: IP spoofing
- Tools like **Wireshark** show encapsulated data, allowing analysts to:
    - Inspect headers
    - Detect anomalies
    - Identify malicious payloads

---

### Exam Key Points

- Encapsulation = **adding headers**
- Decapsulation = **removing headers**
- Each layer has a **specific PDU**
- MAC addresses change hop-to-hop, IP addresses do not

## ***Data Link Layer (OSI Layer 2)***

### Introduction

- The **Data Link Layer** is the **second layer** of the OSI model.
- It is responsible for **reliable data transfer between two directly connected devices**.
- This layer ensures that data sent from the Network Layer is **properly formatted, addressed, and error-checked** before transmission.

---

## Functions of the Data Link Layer

1. **Framing**
    - Divides raw data into manageable units called **frames**.
    - Each frame contains source and destination information.
2. **Physical Addressing**
    - Uses **MAC addresses** to identify devices on a local network.
3. **Error Detection**
    - Detects transmission errors using **Frame Check Sequence (FCS)**.
4. **Flow Control**
    - Prevents fast senders from overwhelming slow receivers.
5. **Media Access Control**
    - Controls how multiple devices share the same transmission medium.

---

## Ethernet

### What is Ethernet?

- **Ethernet** is the most common **LAN technology**.
- Defined by **IEEE 802.3** standards.
- Operates mainly at the **Data Link Layer**, with some Physical Layer involvement.

### Ethernet Characteristics

- Uses **MAC addresses** for device identification
- Uses **frames** as PDUs
- Supports speeds from **10 Mbps to 100+ Gbps**
- Common in homes, offices, and data centers

### Ethernet Frame Structure

- **Preamble** – Synchronizes sender and receiver
- **Destination MAC Address**
- **Source MAC Address**
- **Type/Length field**
- **Payload (Data)**
- **Frame Check Sequence (FCS)** – Error detection

---

## Transmission Media

### 1. Copper Cable

### Description

- Uses **electrical signals** to transmit data.
- Most common medium in Ethernet LANs.

### Types of Copper Cables

- **UTP (Unshielded Twisted Pair)**
- **STP (Shielded Twisted Pair)**

### Common Categories

- **Cat5e** – Up to 1 Gbps
- **Cat6** – Up to 10 Gbps (short distance)
- **Cat6a** – Up to 10 Gbps (long distance)

### Advantages

- Low cost
- Easy to install and maintain

### Disadvantages

- Susceptible to **electromagnetic interference (EMI)**
- Limited distance (100 meters)

---

### 2. Fiber Optic Cable

### Description

- Uses **light pulses** instead of electrical signals.
- Core made of glass or plastic.

### Types of Fiber

- **Single-Mode Fiber**
    - Long-distance transmission
    - Very high bandwidth
- **Multi-Mode Fiber**
    - Shorter distance
    - Lower cost than single-mode

### Advantages

- Immune to EMI
- Very high speed
- Secure and difficult to tap

### Disadvantages

- Expensive
- Complex installation and repair

---

### 3. Wireless Media

### Description

- Uses **radio waves** to transmit data.
- Commonly used in Wi-Fi networks (**IEEE 802.11**).

### Characteristics

- Provides mobility and flexibility
- More interference-prone
- Less secure than wired media

---

## Network Interface Card (NIC)

### Definition

- A **NIC** is a hardware component that connects a device to a network.
- Can be **wired (Ethernet)** or **wireless (Wi-Fi)**.

### Functions of a NIC

- Stores the device’s **MAC address**
- Converts data into electrical, light, or radio signals
- Handles frame transmission and reception

---

## Media Access Control (MAC)

### MAC Sub-layer

- A sub-layer of the Data Link Layer.
- Controls how devices **access the shared transmission medium**.

### Responsibilities

- Assigning MAC addresses
- Frame encapsulation
- Collision handling

---

## MAC Address

### Definition

- A **MAC (Media Access Control) address** is a **unique hardware identifier** assigned to a NIC.
- Used for communication **within a local network**.

### Characteristics

- Length: **48 bits (6 bytes)**
- Written in **hexadecimal format**
- Example: `A4:5E:60:9F:12:BC`

---

## MAC Address Structure

| Part | Size | Description |
| --- | --- | --- |
| OUI (Organizationally Unique Identifier) | 24 bits | Identifies manufacturer |
| Device Identifier | 24 bits | Uniquely identifies the device |
- OUI is assigned by **IEEE**.
- Ensures global uniqueness of MAC addresses.

---

## Cybersecurity Relevance of Data Link Layer

- **MAC spoofing** – Attacker changes MAC address
- **ARP poisoning** – Exploits Layer 2 address resolution
- **Packet sniffing** using Wireshark
- **Switch attacks** (MAC flooding)

---

## Exam-Oriented Key Points

- Data Link Layer PDU = **Frame**
- Ethernet standard = **IEEE 802.3**
- MAC addresses operate only within a LAN
- Fiber is fastest and most secure
- Wireless media is convenient but vulnerable

# ***Network Characteristics***

### Introduction

- **Network characteristics** describe how well a network performs.
- They are critical for evaluating **speed, reliability, and quality** of communication.
- In cybersecurity and networking, these metrics help identify **performance issues, attacks, and faults**.

---

## 1. Bandwidth

### Definition

- **Bandwidth** is the **maximum data-carrying capacity** of a network link.
- It represents the **theoretical maximum speed** of a network.

### Key Points

- Measured in **bits per second (bps)**
- Common units: Mbps, Gbps
- Depends on:
    - Transmission medium
    - Network hardware

### Important Note

- High bandwidth does **not** guarantee high performance if the network is congested.

---

## 2. Throughput

### Definition

- **Throughput** is the **actual amount of data successfully transmitted** over a network in a given time.
- It is always **less than or equal to bandwidth**.

### Measurement

- Measured in **bps, Mbps, or Gbps**
- Affected by:
    - Network congestion
    - Packet loss
    - Latency
    - Protocol overhead

### Bandwidth vs Throughput

- Bandwidth = capacity
- Throughput = real performance

---

## 3. Measuring Throughput

### Methods

- File transfer tests
- Speed test tools
- Network monitoring tools

### Factors Affecting Throughput

- Number of users
- Hardware limitations
- Network attacks (DoS, flooding)

---

## 4. Latency

### Definition

- **Latency** is the **time taken for a packet to travel from source to destination**.
- Also called **delay**.

### Measured In

- **Milliseconds (ms)**

### Causes of Latency

- Distance between devices
- Routing paths
- Network congestion
- Processing delays

---

## 5. Round Trip Time (RTT)

### Definition

- **RTT** is the time taken for a packet to go from sender to receiver **and back again**.

### Importance

- Used to measure network responsiveness
- Critical for real-time applications

---

## 6. Ping

### What is Ping?

- **Ping** is a network utility used to test **connectivity and RTT**.
- Uses the **ICMP protocol**.

### Purpose of Ping

- Check if a host is reachable
- Measure latency and RTT
- Detect packet loss

### Ping Utility (Terminal)

### Windows

```
ping google.com

```

### Linux / macOS

```
ping google.com

```

### Ping Output Shows

- Time taken (latency)
- Packets sent and received
- Packet loss percentage

---

## 7. Jitter

### Definition

- **Jitter** is the **variation in packet delay**.
- Indicates inconsistency in latency.

### Why Jitter Matters

- Affects real-time applications:
    - VoIP
    - Video calls
    - Online gaming

### Causes of Jitter

- Network congestion
- Route changes
- Buffering delays

---

## 8. Packet Loss

### Definition

- **Packet loss** occurs when data packets **fail to reach their destination**.

### Causes

- Network congestion
- Faulty hardware
- Wireless interference
- Attacks (DoS)

### Effects

- Reduced throughput
- Retransmissions (TCP)
- Poor application performance

---

## 9. Packet Loss Rate

### Definition

- **Packet loss rate** is the **percentage of packets lost** during transmission.

### Formula

- Packet Loss Rate = (Lost Packets / Total Sent Packets) × 100

### Acceptable Levels

- 0–1%: Excellent
- 1–2%: Acceptable
- 2%: Poor network quality

---

## Cybersecurity Relevance

- High latency and packet loss may indicate **network attacks**
- Jitter spikes can signal **traffic manipulation**
- Throughput drops may indicate **DoS or bandwidth abuse**

---

## Exam-Oriented Key Points

- Bandwidth ≠ Throughput
- Latency and RTT are time-based metrics
- Ping uses ICMP
- Jitter affects real-time communication
- Packet loss degrades reliability