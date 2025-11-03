
### 1. Compare and contrast the basic principles of distance-vector routing and link-state routing algorithms

| Feature                | Distance-Vector Routing       | Link-State Routing                |
|------------------------|------------------------------|-----------------------------------|
| Knowledge              | Only neighbors' information   | Complete network topology         |
| Updates                | Periodic, entire table        | Event-driven, only changes        |
| Algorithm Used         | Bellman-Ford                 | Dijkstra's shortest path algorithm|
| Traffic Overhead       | Less, but periodic            | More, but only during changes     |
| Convergence            | Slower (count-to-infinity)   | Faster                            |
| Memory Requirements    | Lower                        | Higher                            |
| Scalability            | Scales less well             | Scales better                     |
| Example Protocols      | RIP                          | OSPF                              |

**Key Points:**
- Distance-vector protocols share only distance (cost) and next-hop info to neighbors; link-state protocols broadcast link info to all routers so everyone keeps a full map.
- Link-state is preferred in large, complex networks due to speed and flexibility, while distance-vector works for smaller, simpler topologies[1][2].

***

### 2. Describe the operation of the TCP congestion control algorithm and how it helps prevent network congestion

**TCP Congestion Control Phases:**
- **Slow Start:** Initially, sender sets congestion window (cwnd) to 1 MSS (Maximum Segment Size), doubles each RTT.
- **Congestion Avoidance:** Once a threshold is reached, cwnd increases linearly.
- **Congestion Detection:** On timeout, cwnd resets to 1 MSS, threshold set to half of previous cwnd.
- **Fast Retransmit/Fast Recovery:** On 3 duplicate ACKs, threshold is halved, but cwnd set to threshold (cuts congestion quickly, maintains throughput).

**How it prevents congestion:**
- Adapts transmission rate to network conditions, avoids swamping network.
- Uses acknowledgments and windowing to probe available bandwidth and back off when packet loss is detected[1][3].

***

### 3. How does classful addressing work in IPv4 and what limitations does it have?

**Classful Addressing:**
- Divides IP address space into Classes A, B, C, D, E.
- Class determined by leading bits.
- Network/host fields fixed by class:
  - A: Large networks, many hosts (0.0.0.0 - 127.255.255.255)
  - B: Medium networks (128.0.0.0 – 191.255.255.255)
  - C: Small networks (192.0.0.0 – 223.255.255.255)
  - D: Multicast, E: Reserved

**Limitations:**
- Inefficient address use—fragmented, wasted space.
- Inflexible for modern networks—cannot aggregate or subdivide efficiently.
- Rapid exhaustion of IPv4 address space led to creation of CIDR (Classless InterDomain Routing)[2].

***

### 4. Explain the structure of the IPv4 header and describe the purpose of each field

| Field              | Size (bits) | Purpose                                          |
|--------------------|-------------|--------------------------------------------------|
| Version            | 4           | Protocol version (4 for IPv4)                    |
| IHL                | 4           | Header length (words)                            |
| Type of Service    | 8           | Traffic type/prioritization                      |
| Total Length       | 16          | Total length (header + data)                     |
| Identification     | 16          | Unique ID for fragmentation/reassembly           |
| Flags              | 3           | Fragmentation control                            |
| Fragment Offset    | 13          | Position of fragment in original datagram        |
| Time to Live (TTL) | 8           | Hop count limit, prevents looping                |
| Protocol           | 8           | Type of carried protocol (TCP, UDP, etc.)        |
| Header Checksum    | 16          | Error check for header                           |
| Source Address     | 32          | Sender’s IP address                              |
| Destination Address| 32          | Receiver’s IP address                            |
| Options / Padding  | Variable    | For future use, alignment                        |

**Diagram:**
```
|Ver|IHL|TOS| Total Length |....| TTL|Protocol|Checksum| Src Addr | Dst Addr |Options|
```


***

### 5. Describe how the transport layer ensures reliable data delivery between end systems

**Reliability Mechanisms:**
- **Sequencing:** All bytes/segments are numbered.
- **Acknowledgments:** Receiver sends back ACKs; sender retransmits if not received.
- **Timers:** Sender sets timers for ACKs; if timeout, triggers retransmission.
- **Checksums:** For each segment, detects errors.
- **Sliding Window:** Manages how much data can be in flight.
- **Duplicate Filtering:** Detects and drops duplicates.
- **Reordering:** Handles out-of-order segments at receiver.

**Illustration:**
```
Sender Segment -> [Receiver] -> ACK -> [Sender]
           <--------------------------->
Timeout/No-ACK: Retransmit segment
```


***

### 6. What is the TCP three-way handshake, and why is it important for establishing a connection?

**Process:**
1. **SYN:** Client sends SYN (synchronize) to server.
2. **SYN-ACK:** Server responds with SYN-ACK.
3. **ACK:** Client sends ACK, connection is established.

**Why Important:**
- Ensures each side is ready with correct sequence numbers.
- Allows duplex synchronization so both parties agree to connection[1][3].

***

### 8. Explain the structure of a UDP segment and describe the purpose of each field

| Field                  | Size (bits) | Purpose                                    |
|------------------------|-------------|--------------------------------------------|
| Source Port            | 16          | Sender’s port number                       |
| Destination Port       | 16          | Recipient’s port number                    |
| Length                 | 16          | Total segment length (header + data)       |
| Checksum               | 16          | Detects errors in header/data              |

- Fixed 8-byte header.
- Simpler, lower overhead compared to TCP.

Diagram:
```
| Src Port | Dst Port | Length | Checksum | Data ... |
```
.

***

### 10. Design a scenario where SCTP would be more beneficial than TCP or UDP. How would you leverage SCTP’s multi-streaming and multi-homing capabilities?

**Scenario:**
- Voice/video conferencing, where data loss should not break all streams (e.g., video continues if audio drops).
- Multi-homed servers (multiple network connections for redundancy).

**Leveraging SCTP:**
- **Multi-streaming:** Application splits data into logical streams; message loss in one does not block others.
- **Multi-homing:** SCTP endpoint binds to multiple IPs; can reroute traffic if one link fails, increasing reliability and availability[1].

***

### 12. How does a web browser interact with web servers to retrieve and display web pages? Explain the process in detail.

**Steps:**
- User enters URL in browser.
- Browser uses DNS to translate domain name to IP address.
- Browser opens TCP connection to server (port 80 for HTTP, 443 for HTTPS).
- Sends HTTP request (GET/POST).
- Server responds with HTTP response (headers and body).
- Browser interprets HTML, CSS, JS to render page for user.

**Diagram:**
```
[User]--(URL)-->[Browser]--(DNS)-->[DNS Server]--(IP)-->[Web Server]
                           ^---(HTTP Request)-----> [Web Server]
                           <----(HTTP Response)---/
```


***

### 14. How does HTTP handle communication between a web browser (client) and a web server?

- HTTP is a stateless, application-layer protocol.
- Uses request-response model:
  - Client sends request (e.g., GET, POST) to server.
  - Server replies with response (status, headers, body).
- Operates over TCP (ensures reliable delivery).
- Each transaction is independent (unless using persistent 'keep-alive' connections or cookies/sessions for continuity)[3].

***

### 15. Explain the purpose of the Domain Name System (DNS) and how it translates human-readable domain names into IP addresses.

- DNS is a distributed database that maps domain names to IP addresses.
- Client (resolver) queries DNS server for an address (e.g., www.example.com).
- Server responds with the corresponding IP (e.g., 192.0.2.1).
- If not found, server refers to higher-level or authoritative server.
- Makes the Internet user-friendly and scalable[3].

**Diagram:**
```
[User: www.example.com] -> [Resolver] -> [DNS Server] -> [Authoritative DNS] -> [IP Address]
```
***

### 16. What is remote logging, and how does it help in monitoring and troubleshooting networked systems?

- **Remote logging**: Process where system logs are sent over the network to a centralized server.
- Enables centralized monitoring, auditing, and troubleshooting of distributed systems.
- Essential for real-time alerting, compliance, and forensics in the event of errors or security breaches[3].

***

If you need detailed answers or illustrative diagrams for specific questions, or want tables formatted for printing/presentation, let me know which ones to focus on!

Citations:
[1] Unit-4-CN.docx https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/87014956/91e8f031-0c93-4e52-a5a2-e87310bf912e/Unit-4-CN.docx
[2] unit-3-cn-1.docx https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/87014956/3c1b8898-c0d5-4064-b5f5-ea56a39fdc51/unit-3-cn-1.docx
[3] Cn-unit5.pdf https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/87014956/52d3e75f-2c11-4848-b2c9-671849e2f48f/Cn-unit5.pdf
[4] 1000158693.jpeg https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/images/87014956/683cd666-5be8-40fc-813c-7ba76f0c7baf/1000158693.jpeg


## Q1: Distance-Vector vs Link-State Routing

**Distance-vector** routers use neighbor info and exchange vectors periodically. **Link-state** routers build a complete map of the network with link info, running algorithms like Dijkstra’s for best paths.

**Comparison Table:**

| Feature                | Distance-Vector            | Link-State                |
|------------------------|---------------------------|---------------------------|
| Info Shared            | Vectors w/ neighbors      | Complete link-state map   |
| Network View           | Local                     | Global                    |
| Algorithm              | Bellman-Ford              | Dijkstra’s                |
| Convergence Speed      | Slow                      | Fast                      |
| Resource Usage         | Low                       | High                      |
| Loops                  | Persistent possible       | Mainly transient          |

**Illustrative Diagram:**  
[1][2]

***

## Q2: TCP Congestion Control Operation

TCP employs **Slow Start, Congestion Avoidance, and Congestion Detection** (additive increase/multiplicative decrease) to dynamically adjust traffic rate.

**Phases Table:**

| Phase                | Behavior                                     |
|----------------------|----------------------------------------------|
| Slow Start           | Rapid exponential growth of cwnd             |
| Avoidance            | Linear increase after threshold              |
| Detection            | Drops on loss, resets cwnd or reduces window |

**Diagram:**  
[3][4]

***

## Q3: Classful Addressing in IPv4

IPv4 originally used **classful addressing** (A-E), where address blocks are split by prefix bits.

**Structure Table:**

| Class | Leading Bits | Net Bits | Host Bits | Example Address | Usable Host Count |
|-------|--------------|----------|-----------|----------------|-------------------|
| A     | 0            | 8        | 24        | 10.x.x.x        | ~16 million       |
| B     | 10           | 16       | 16        | 172.16.x.x      | ~65,000           |
| C     | 110          | 24       | 8         | 192.168.1.x     | 256               |
| D     | 1110         | -        | -         | multicast       | -                 |
| E     | 1111         | -        | -         | reserved        | -                 |

**Diagram:**  
[5]

***

## Q4: IPv4 Header Structure

The **IPv4 header** is a 20-byte structured block with fields for addressing, control, and routing.

**Header Fields Table:**

| Field            | Bits | Purpose                                |
|------------------|------|----------------------------------------|
| Version          | 4    | IPv4 identifier                        |
| IHL              | 4    | Header length                          |
| Type of Service  | 8    | Handling priorities                    |
| Total Length     | 16   | Datagram length                        |
| Identification   | 16   | Datagram reassembly                    |
| Flags            | 3    | Fragmentation controls                 |
| Fragment Offset  | 13   | Datagram fragment location             |
| TTL              | 8    | Lifetime                               |
| Protocol         | 8    | Next-level protocol indicator          |
| Header checksum  | 16   | Header error checking                  |
| Source address   | 32   | Sender address                         |
| Destination addr | 32   | Recipient address                      |
| Options          | var  | Special functionalities                |

**Diagram:**  
[6][7]

***

## Q5: Transport Layer Reliability

The transport layer, especially TCP, uses connection management, sequencing, flow/error control, and retransmission for reliability.

**Mechanism Table:**

| Mechanism         | Role                                         |
|-------------------|-----------------------------------------------|
| Connection        | Ensures session management                   |
| Numbering/ORDER   | Ensures proper sequence and integrity        |
| Flow Control      | Avoids receiver overload                     |
| Error Control     | Uses checksum, ACK, and retransmission       |

**Diagram:**  
[8][9]

***

## Q6: TCP Three-Way Handshake

A **three-stage exchange** (SYN, SYN-ACK, ACK) between client and server establishes session and synchronizes sequence numbers.

**Steps Diagram:**  
[10][11]

***

## Q7: UDP Segment Structure

UDP is a **lightweight protocol** with a minimal 8-byte header.

**Header Table:**

| Field          | Bits | Example Value      |
|----------------|------|-------------------|
| Source Port    | 16   | 12345             |
| Destination Port | 16 | 80                |
| Length         | 16   | 32                |
| Checksum       | 16   | 0x1a2b            |

**Diagram:**  
[12][13]

***

## Q8: SCTP Use Case

*Not enough details in source to compare SCTP features or leverage multi-streaming.*

***

## Q9: Web Browser-Server Interaction

User types a URL, browser resolves DNS, opens TCP session to server, sends HTTP request, receives HTTP response, renders content, and closes connection.

**Summary Table:**

| Step                 | Explanation                                 |
|----------------------|---------------------------------------------|
| User Input           | Browser receives URL                        |
| DNS Resolution       | Finds IP address                            |
| TCP Connection       | 3-way handshake to server                   |
| HTTP Request         | Browser requests page                       |
| Server Response      | Server sends HTML/data                      |
| Rendering            | Browser displays content                    |
| Connection End       | TCP session closes                          |

**Diagram:**  
[14][15]

***

## Q10: HTTP Communication Model

HTTP uses a simple request-response over TCP where client sends a method+URL, receives a status+body, and session is stateless.

**Message Table:**

| Message Type | Example Start Line          |
|--------------|----------------------------|
| Request      | GET /index.html HTTP/1.1   |
| Response     | HTTP/1.1 200 OK            |

**Diagram:**  
[14]

***

## Q11: DNS: Domain Names to IPs

DNS translates human-readable names into machine IPs by querying a distributed, hierarchical set of servers.

**Process Table:**

| Step                 | Explanation                                    |
|----------------------|------------------------------------------------|
| Query                | User enters name, DNS resolver queried         |
| Hierarchy            | TLD/root servers escalate as needed            |
| Response             | Resolver returns IP address for host           |

**Diagram:**  
[14]

***

*All diagram sources referenced above for illustration. For full-size and updated images, follow source links.*

Citations:
[1] Distance Vector Routing v/s Link State Routing - Scaler Blog https://www.scaler.in/distance-vector-routing-v-s-link-state-routing/
[2] Distance Vector Routing vs Link State Routing https://data-flair.training/blogs/distance-vector-routing-vs-link-state-routing/
[3] TCP Congestion Control - Scaler https://www.scaler.com/topics/computer-network/tcp-congestion-control/
[4] TCP Congestion Control - GeeksforGeeks https://www.geeksforgeeks.org/computer-networks/tcp-congestion-control/
[5] Classful network https://en.wikipedia.org/wiki/Classful_network
[6] IPv4 Header Format, Diagram, and its Significance - PyNet Labs https://www.pynetlabs.com/introduction-to-ipv4-header-format/
[7] IPv4 Datagram Header - GeeksforGeeks https://www.geeksforgeeks.org/computer-networks/introduction-and-ipv4-datagram-header/
[8] Transport Layer https://www.networkacademy.io/ccna/network-fundamentals/transport-layer
[9] Transport Layer in OSI Model https://www.geeksforgeeks.org/computer-networks/transport-layer-in-osi-model/
[10] TCP_3_way_handshaking https://wiki.wireshark.org/TCP_3_way_handshaking
[11] TCP 3-Way Handshake Process https://www.geeksforgeeks.org/computer-networks/tcp-3-way-handshake-process/
[12] Examples on UDP Header https://www.geeksforgeeks.org/computer-networks/examples-on-udp-header/
[13] User Datagram Protocol - UDP https://www.geeksforgeeks.org/computer-networks/user-datagram-protocol-udp/
[14] HTTP messages - MDN Web Docs - Mozilla https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Messages
[15] HTTP Request Response Flow - Parth Goswami https://www.parthgoswami.com/http_request_response_flow/
[16] Difference between Distance vector routing and Link State ... https://www.geeksforgeeks.org/computer-networks/difference-between-distance-vector-routing-and-link-state-routing/
[17] Difference between Distance Vector Routing and Link ... https://www.tutorialspoint.com/difference-between-distance-vector-routing-and-link-state-routing
[18] Link State vs Distance Vector vs Hybrid Routing Protocols https://www.cbtnuggets.com/blog/technology/networking/link-state-distance-vector-vs-hybrid-routing-protocols
[19] CN 20 : Distance Vector VS Link State Routing | Examples https://www.youtube.com/watch?v=0Q3SEa9qyAI
[20] Introduction of Classful IP Addressing https://www.geeksforgeeks.org/computer-networks/introduction-of-classful-ip-addressing/
