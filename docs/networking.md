# Networking Basics

## 🔹 IP Addressing (Layer 3 - Network Layer)
An **IP address** is a unique identifier assigned to each device on a network, allowing communication between devices. IP operates at **Layer 3 (Network Layer)** of the OSI model.

### IPv4
- **32-bit address space** → Supports **2³² (~4.2 billion)** unique addresses.
- Address format: **`xxx.xxx.xxx.xxx`** (four octets, each 8 bits).
- Due to address exhaustion, IPv4 requires techniques like **NAT (Network Address Translation)**.

### IPv6
- **128-bit address space** → Supports **2¹²⁸** addresses (virtually unlimited).
- Address format: **`xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx`** (hexadecimal).
- Designed to replace IPv4, but adoption is ongoing.

### Why Are We Still Using IPv4?
Due to address exhaustion, **NAT (Network Address Translation)** allows multiple devices in a private network to share a single public IPv4 address. This helps extend the usability of IPv4.

---

## 🔹 Private IPv4 Address Ranges
IPv4 addresses are categorized into different **classes**, with specific private IP ranges:

| Class  | Address Range                   | Number of Hosts  |
|--------|----------------------------------|------------------|
| **A**  | `10.0.0.0 – 10.255.255.255`     | 16 million       |
| **B**  | `172.16.0.0 – 172.31.255.255`   | 65,000           |
| **C**  | `192.168.0.0 – 192.168.255.255` | 254              |

These private addresses **cannot** be routed on the public internet and require NAT for external communication.

---

## 🔹 MAC Addressing (Layer 2 - Data Link Layer)
A **MAC address** (Media Access Control address) is a **48-bit unique identifier** assigned to network interfaces and operates at **Layer 2 (Data Link Layer)** of the OSI model.

- Format: **`XX:XX:XX:XX:XX:XX`** (six pairs of hexadecimal digits).
- The first three pairs (**OUI - Organizationally Unique Identifier**) identify the manufacturer.
- You can look up MAC addresses using online databases.

---

## 🔹 TCP vs. UDP (Layer 4 - Transport Layer)

### **TCP (Transmission Control Protocol)**
- **Connection-oriented** protocol (ensures reliable communication).
- Uses a **3-way handshake** to establish a connection:
  1. **SYN** → Client sends a request to initiate communication.
  2. **SYN-ACK** → Server acknowledges the request.
  3. **ACK** → Client confirms the connection is established.
- **Use case:** Web browsing (HTTP/HTTPS), emails (SMTP/IMAP/POP3), file transfers (FTP).

### **UDP (User Datagram Protocol)**
- **Connectionless** protocol (faster but unreliable).
- No handshake; packets are sent without guarantee of arrival.
- **Use case:** Video streaming, VoIP calls, online gaming (low-latency applications).

---

## 🔹 OSI Model - 7 Layers
The **OSI (Open Systems Interconnection) Model** standardizes communication functions across networks.

| Layer | Name                  | Function & Protocols               |
|-------|----------------------|----------------------------------|
| **7** | Application          | HTTP, HTTPS, FTP, SMTP, DNS     |
| **6** | Presentation         | Encryption, SSL/TLS, ASCII      |
| **5** | Session             | Manages connections (RPC, NetBIOS) |
| **4** | Transport            | TCP, UDP                        |
| **3** | Network              | IP, ICMP, ARP, RIP              |
| **2** | Data Link            | MAC addresses, Ethernet         |
| **1** | Physical             | Cables, NICs, Wi-Fi             |

Each layer provides specific functionality to ensure smooth data transmission.

---

## 🔹 Subnetting
**Subnetting** divides a large network into smaller sub-networks (subnets) to improve efficiency and security.

### **Key Concepts:**
- **Subnet Mask**: Determines how many bits are used for the **network** vs. **hosts**.
- **CIDR (Classless Inter-Domain Routing)**: Defines subnet masks using `/` notation (e.g., `192.168.1.0/24`).
- **Whack (`/` Notation)**: The number after `/` indicates how many bits belong to the network.

### **Subnet Mask Breakdown**
| CIDR Notation | Subnet Mask       | # of Hosts |
|--------------|-----------------|------------|
| `/8`         | `255.0.0.0`     | 16M hosts  |
| `/16`        | `255.255.0.0`   | 65K hosts  |
| `/24`        | `255.255.255.0` | 254 hosts  |

For subnetting calculations, **IP calculators** like [IPaddressguide.com](https://www.ipaddressguide.com/cidr) help determine IP ranges and hosts available.

---

## 🔹 Common Network Protocols & Ports
### **Well-Known Ports:**
| Protocol | Port | Description |
|----------|------|-------------|
| HTTP     | 80   | Web traffic (unencrypted) |
| HTTPS    | 443  | Secure web traffic (SSL/TLS) |
| FTP      | 21   | File transfer |
| SSH      | 22   | Secure shell access |
| DNS      | 53   | Domain name resolution |
| DHCP     | 67/68 | Dynamic IP allocation |
| SMTP     | 25   | Email sending |
| IMAP     | 143  | Email retrieval |
| RDP      | 3389 | Remote desktop protocol |

---

## 🔹 Conclusion
Understanding **IP addressing, MAC addresses, TCP/UDP, OSI model, and subnetting** is essential for networking. Subnetting efficiently divides networks, while protocols ensure seamless communication. By leveraging these concepts, network engineers and security professionals can design and troubleshoot robust networks effectively.