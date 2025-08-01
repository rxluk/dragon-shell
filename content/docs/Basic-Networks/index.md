---
title: 'General Guide to Networking'
description: >
  A complete and practical guide to understanding the main network protocols, how they work, and how to analyze them in the real world.
date: '2025-08-01T15:10:00-03:00'
draft: false
tags:
  - networking
  - protocols
  - tcpip
  - dns
categories:
  - docs
authors:
  - luk
cover:
  image: pattern.png
---

If you want to work with offensive security, system administration, web development, or simply understand how the internet really works, you need to master **network protocols**.

In this guide, we’ll explore everything from protocol analyzers to DNS, covering TCP/IP, Ethernet, ARP, IP, TCP, UDP, and HTTP.

---

## 🔍 Protocol Analyzers

Protocol analyzers let you see and study the actual traffic flowing through the network. Tools like **Wireshark** and **tcpdump** display packets, headers, and data in real time.

### Examples:
```bash
sudo tcpdump -i eth0
sudo tcpdump -n host 8.8.8.8
```

In **Wireshark**, you can filter like this:
```
http
dns
tcp.port == 80
```

These tools are essential for forensics, troubleshooting, and security analysis.

---

## 🌐 Introduction to TCP/IP

**TCP/IP** is the foundation of internet communication. It organizes data transmission into layers:

1. **Application** – protocols like HTTP, FTP, DNS  
2. **Transport** – TCP, UDP  
3. **Internet** – IP, ICMP, ARP  
4. **Link** – Ethernet, Wi-Fi  

Each layer has specific roles and protocols to ensure standardized communication.

---

## 📡 Network Protocols

Network protocols are standardized "languages" that machines use to communicate.  
Without them, every manufacturer would use their own method and nothing would work together.

---

## 🖧 Ethernet Protocol

**Ethernet** works at the link layer. It wraps IP packets into Ethernet frames, which include:

- **Source MAC address**
- **Destination MAC address**
- **Encapsulated protocol type**

### View MAC addresses:
```bash
ip link show
```

Ethernet is mostly used in LANs, cables, and switches.

---

## 🧠 ARP Protocol

**ARP (Address Resolution Protocol)** maps an IP address to a MAC address.  
When a device wants to talk to another on the same network, it uses ARP to discover the MAC address.

### Show ARP table:
```bash
arp -a
ip neigh
```

### Common attack:
- **ARP Spoofing** – sends fake ARP replies to intercept traffic (Man-in-the-Middle).

---

## 📬 IP Protocol

**Internet Protocol** handles addressing and routing of packets.

- **IPv4**: 32-bit addresses (e.g., `192.168.0.1`)
- **IPv6**: 128-bit addresses (e.g., `2001:db8::1`)

### IPv4 address types:
- **Public**: reachable over the internet
- **Private**: used in local networks (`192.168.x.x`, `10.x.x.x`, `172.16.x.x` to `172.31.x.x`)

---

## 📦 TCP Protocol

**Transmission Control Protocol** is **connection-oriented**.  
It ensures reliable data delivery, retransmits lost packets, and maintains order.

Key features:
- 3-way handshake (SYN, SYN-ACK, ACK)
- Flow control
- Acknowledgment (ACK)

### Check active TCP connections:
```bash
netstat -ant
ss -t
```

---

## ⚡ UDP Protocol

**User Datagram Protocol** is **connectionless**.  
It does not guarantee delivery or order, but it’s much faster.

Used in:
- Video streaming
- Online gaming
- DNS
- VoIP

---

## 🌐 HTTP Protocol

**HyperText Transfer Protocol** is used for communication between browsers and web servers.

### Example HTTP request:
```
GET /index.html HTTP/1.1
Host: example.com
```

Today, we mostly use **HTTPS**, which adds encryption via TLS.

---

## 🧭 DNS – Domain Name System

**DNS** converts names like `google.com` into IPs like `142.250.69.206`.

### Basic flow:
1. Browser asks the **local resolver** (usually your router).
2. If not cached, it queries **root servers**.
3. Root servers point to **TLD servers** (`.com`, `.org`, `.br`).
4. TLDs point to **authoritative servers** for the domain.
5. IP response returns to the client.

### Useful commands:
```bash
dig google.com
nslookup github.com
host openai.com
```

### Record types:
- **A**: points to IPv4 address
- **AAAA**: points to IPv6 address
- **MX**: mail server
- **CNAME**: alias
- **TXT**: texts, SPF/DKIM

---

## 🔒 Protocol Security

Some common vulnerabilities:
- **ARP Spoofing** – poisons the ARP table.
- **DNS Spoofing/Poisoning** – responds with fake IP.
- **Sniffing** – captures unencrypted TCP/HTTP traffic.
- **Injection** – exploits poorly configured protocols.

---

## 🧪 Hands-on Practice

- Use **Wireshark** to observe real traffic.
- Capture a TCP handshake.
- Watch a DNS query in action.
- See how HTTP packets look without encryption.

Exploring protocols hands-on will cement your knowledge far more than just reading about them.

---

Understanding protocols is like speaking the internet's native language. It’s what separates someone who uses the network from someone who **masters** it.
