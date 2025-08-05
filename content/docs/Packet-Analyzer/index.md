---
title: 'Packet Analysis'
description: >
  Uncovering Network Traffic and Understanding Every Packet on Your Network.
date: '2025-08-05T16:00:00-03:00'
draft: false
tags:
  - networking
  - protocols
  - packet-analysis
  - tcpdump
categories:
  - docs
authors:
  - luk
cover:
  image: pattern.png
---

# Packet Analysis: Uncovering Network Traffic

In our **General Guide to Networking**, we explored the theory behind the protocols that make the internet work.  
But what if I told you it’s possible to go beyond theory and actually see the conversations happening on your network?

That’s exactly what we’re doing here. This post is a deep dive into the art of reading network traffic.

We'll use tools like `tcpdump` to break down what each line means, understand every part of a packet, and most importantly, figure out **what we can and can’t see**.

By the end, you'll be able to speak the "language" of the network and analyze packets like a pro.

---

## The Anatomy of a Packet

Before we dive into `tcpdump` output, let’s break down the basic structure of a network packet.

Think of a packet like a letter:

- **Header**: The envelope. It contains important routing info like source/destination addresses and the type of data.
- **Payload**: The actual message inside the envelope — the data your app is trying to send (a web page, a video chunk, a message, etc).

Our goal is to learn how to read both the **envelope** and, when possible, the **content** of these packets.

---

## Decoding `tcpdump` Output

`tcpdump` is a powerful command-line tool to capture and analyze network traffic.

Let’s dissect a real example:
```bash
15:57:09.259316 IP 172.31.40.200.60262 > 13.107.246.33.https: Flags [.], ack 2954965298, win 501, length 0
```

**Breakdown:**

- `15:57:09.259316`: Timestamp when the packet was captured.
- `IP`: Protocol used — in this case, IPv4.
- `172.31.40.200.60262`: Source IP and port.
- `>`: Traffic direction — from source to destination.
- `13.107.246.33.https`: Destination IP and port (443 translated as `https`).
- `Flags [.]`: TCP flags — in this case, just ACK.
- `ack 2954965298`: Acknowledgment number — tells which byte the receiver expects next.
- `win 501`: Receive window — how much data the receiver can accept before sending another ACK.
- `length 0`: No payload — this is a control-only packet.

---

## Example: DNS Query

Here’s another example, this time with DNS:
```bash
15:57:09.319786 IP 172.31.40.200.45821 > rxluk.home.net.domain: 37311+ PTR? 33.246.107.13.in-addr.arpa. (44)
```

**Breakdown:**

- `rxluk.home.net.domain`: Destination resolved DNS name (port 53).
- `37311+`: DNS query ID with recursion requested (`+`).
- `PTR?`: Reverse DNS lookup (finding a hostname from an IP).
- `33.246.107.13.in-addr.arpa.`: Format used for reverse lookups.
- `(44)`: Total size of the query in bytes.

---

## Can You Read the Packet? Understanding Encryption

**What you can see depends on the protocol.**

### **Unencrypted Protocols** (HTTP, FTP):
- Full content is visible.
- Sensitive info like passwords and form data can be read by anyone on the same network.
- That’s why they’re considered insecure.

### **Encrypted Protocols** (HTTPS, SSH):
- You only see headers (source/destination IPs, ports, packet size).
- The payload (real content) is **unreadable** without the decryption key.

Understanding this difference is **crucial** for knowing when your data is safe.

---

## Recommended Practice

The best way to learn is by **doing**:

- Use **Wireshark** (GUI) or `tcpdump` (CLI).
- Capture a **TCP handshake** (SYN, SYN-ACK, ACK).
- Observe a **DNS query** happening live.
- Compare **HTTP vs HTTPS** packets to see encryption in action.

---

## Final Thoughts

Understanding network protocols and learning how to read network traffic is like **learning the language of the internet**.

With this guide, you’ve got the tools to begin real-world packet analysis. The rest is practice.

---
