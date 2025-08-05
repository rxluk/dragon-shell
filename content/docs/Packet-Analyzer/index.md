---
title: "Supreme Packet Analysis: From tcpdump to Wireshark"
description: >
  Master packet analysis with this complete guide — learn everything about headers, payloads, tcpdump, Wireshark, and encrypted protocols.
date: 2025-08-05T16:00:00-03:00
draft: false
tags:
  - networking
  - tcpdump
  - wireshark
  - packet-analysis
  - protocols
categories:
  - docs
authors:
  - luk
cover:
  image: network-capture.png
---

# 🧠 Supreme Packet Analysis: From tcpdump to Wireshark

In our **General Networking Guide**, we explored the fundamentals of protocols. Now it's time to go deeper. We're going to **observe, read, and understand the packets** that travel through your network.

This guide is the most comprehensive you'll find: **tcpdump, Wireshark, headers, payloads, encryption, protocols, best practices — all explained in clear English.**

---

## 📦 Anatomy of a Network Packet

A packet is like a letter:

- **Header**: contains addresses, control info, and metadata.
- **Payload**: the content — message, page, file.

OSI Model layers involved:

- **Layer 2 (Data Link)**: MACs, Ethernet.
- **Layer 3 (Network)**: IPs, TTL, fragmentation.
- **Layer 4 (Transport)**: TCP/UDP, ports, flags.
- **Layer 7 (Application)**: HTTP, DNS, etc.

---

## ⚙️ Capture and Analysis Tools

### 1. `tcpdump` (command-line)
```bash
sudo tcpdump -i eth0 -n -vv
```

- `-i eth0`: Interface to monitor.
- `-n`: Don’t resolve names (faster).
- `-vv`: Verbosity (more detail).

### 2. Wireshark (GUI)

- Allows visual filters, flow reconstruction, protocol statistics.
- Ideal for those who want to "see" the traffic visually.

---

## 🧾 Reading tcpdump Output

Example:
```bash
15:57:09.259316 IP 192.168.0.2.60262 > 142.250.184.206.https: Flags [.], ack 123456789, win 501, length 0
```

Breakdown:

- **Timestamp**: 15:57:09.259316
- **Protocol**: IP (IPv4)
- **Source**: 192.168.0.2:60262
- **Destination**: 142.250.184.206:443 (https)
- **Flags**: ACK (`.`)
- **ack**: Acknowledgment number
- **win**: Window size
- **length**: Payload size (0 = control only)

---

## 🏷️ Common TCP Flags

- `[S]`: SYN – connection start
- `[.]`: ACK – acknowledgment
- `[P]`: PSH – push (send immediately)
- `[F]`: FIN – finish/close connection
- `[R]`: RST – reset
- `[U]`: URG – urgent data

---

## 🌐 Example: DNS Packet

```bash
15:57:09.319786 IP 192.168.0.2.45821 > dns.google.domain: 37311+ PTR? 206.184.250.142.in-addr.arpa. (44)
```

- **PTR?**: Reverse DNS lookup
- **37311+**: DNS request ID with recursion enabled
- **dns.google.domain**: DNS server on port 53
- **(44)**: total query size

---

## 🔐 What Can You See?

### Without Encryption (HTTP, FTP):
- Readable headers and payloads
- Passwords, commands, pages

### With Encryption (HTTPS, SSH):
- Only headers visible
- Encrypted payload (unreadable)

**TIP:** You can still see:
- IPs and ports
- Data volume
- Timing and patterns

---

## 🕵️‍♂️ tcpdump Filter Tips

- Capture only HTTP traffic:
  ```bash
  tcpdump -i eth0 port 80
  ```
- Capture traffic from a single IP:
  ```bash
  tcpdump host 192.168.0.5
  ```
- Capture only DNS traffic:
  ```bash
  tcpdump port 53
  ```

---

## 🎨 Wireshark: Visual Tips

- Use **display filters**:
  - `http`, `dns`, `tcp.port == 443`
- Right-click a packet → **Follow → TCP Stream**
- Visualize handshakes, full sessions, SSL, TLS
- **Statistics → Protocol Hierarchy**: see all protocol activity

---

## 🧪 Practice: Real Exercises

1. Capture a full TCP handshake
2. Visit an HTTP site and view contents in Wireshark
3. Observe live DNS traffic
4. Use filters to separate traffic by IP or protocol
5. Compare HTTP and HTTPS packets

---

## 🧰 Common Observable Protocols

- **HTTP**: Fully visible (if not HTTPS)
- **HTTPS**: Only headers (encrypted)
- **DNS**: Visible, except DNS-over-HTTPS
- **SSH**: Only IPs/ports visible
- **SMTP**: Often in plain text (no TLS)
- **FTP**: Plain text, vulnerable

---

## 🧠 Conclusion

Packet analysis is **reading the language of the internet**. Tools like `tcpdump` and Wireshark are essential for anyone working with networks, security, or wanting to understand what happens under the hood.

With this guide, you're ready to:
- Read packets fluently
- Differentiate secure vs insecure traffic
- Identify network issues
- Perform basic security audits

Now it’s time to **observe real traffic**, filter, interpret, and become a true network analyst.

---

**🚀 Happy analyzing!**