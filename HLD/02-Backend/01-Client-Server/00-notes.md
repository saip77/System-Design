# Client-Server Architecture, Networking & Protocols

## 1. The Core Blueprint (Summary)

The web operates on a **Request-Response cycle**:

- **Client** (browser/mobile app) → sends request  
- **Server** (hosts data/logic) → sends response  

### Key Components:
- **IP Address** → Unique identifier of a device
- **DNS (Domain Name System)** → Maps domain names (e.g., `google.com`) to IP addresses
- **Protocols** → Rules governing data transfer (TCP / UDP)

---

## 2. Interview-Style Deep Dive (Simplified Concepts)

### IP Address (Device Identity)

#### IPv4
- 32-bit address (e.g., `192.168.1.1`)
- Limited (~4.3 billion addresses)
- Running out of space

#### IPv6
- 128-bit address (hexadecimal format)
- Massive address space (virtually unlimited)

---

### Public vs Private IP

- **Private IP**
  - Assigned within local networks (home, office)
- **Public IP**
  - Assigned by ISP
  - Visible on the internet

### NAT (Network Address Translation)
- Router maps multiple **Private IPs → One Public IP**
- Enables many devices to share a single internet connection

---

### TCP (Transmission Control Protocol) — *"Reliable Courier"*

- Guarantees:
  - Delivery
  - Order
  - Error checking

#### 3-Way Handshake:
1. SYN  
2. SYN-ACK  
3. ACK  

✅ Reliable  
❌ Higher latency  

---

### UDP (User Datagram Protocol) — *"Fast Broadcaster"*

- No connection setup
- No delivery guarantee
- No ordering

✅ Very fast  
❌ Possible packet loss  

---

## 3. The "Senior Engineer" Lens (Advanced Concepts)

### What Happens When You Type a URL?

1. Check **Browser Cache**
2. Check **OS Cache**
3. Query **DNS Server**
4. Resolve domain → IP
5. Send request to server

---

### TCP Head-of-Line (HoL) Blocking

- If one packet is lost:
  - All subsequent packets are delayed
- Causes increased latency

💡 Solution:
- **QUIC (used in HTTP/3)** → built on UDP to avoid HoL blocking

---

### Anycast vs Unicast

- **Unicast**
  - One IP → One server

- **Anycast**
  - One IP → Multiple servers globally
  - Request routed to nearest server

---

## 4. Real-World Trade-offs

| Feature      | TCP                                   | UDP                                  |
|-------------|----------------------------------------|--------------------------------------|
| Best For    | HTTP/HTTPS, Email, File Transfer       | Gaming, Streaming, VoIP              |
| Trade-off   | Reliability over speed                 | Speed over reliability               |
| Latency     | Higher (handshakes, checks)            | Lower                                |
| Ordering    | Guaranteed                            | Not guaranteed                       |

---

## 5. Tactical Interview Tips

### The "Why" Matters

Example:

**Q:** TCP or UDP for multiplayer gaming?  
**A:**
- Use **UDP** for player movement → speed matters more than perfect accuracy  
- Use **TCP** for transactions → cannot lose critical data  

---

### Common Pitfall

- Ignoring **DNS latency**
- Always consider:
  - DNS lookup time
  - Network distance

💡 Optimization:
- Use **CDN (Content Delivery Network)** to reduce latency

---

### What Interviewers Look For

- Understanding of **NAT**
- Real-world awareness:
  - Many devices share **one Public IP**

❌ Wrong:
> "Every device has a unique public IP"

✅ Correct:
> Devices use private IPs behind NAT

---

### Revision Tip

- **Live Chat App**
  - Use **TCP (WebSockets)**
  - Ensures order + reliability

- **Video Streaming / Zoom**
  - Use **UDP**
  - Prioritize low latency over perfect accuracy

---

## Key Takeaway

- TCP = Reliability  
- UDP = Speed  
- DNS = Discovery  
- NAT = Real-world scalability  

Understanding **how data travels across the network** is foundational for system design interviews.