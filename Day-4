# Day 4: Networking Fundamentals – How Computers Communicate

**Roadmap:** Zero to Hired – Cybersecurity (Month 1, Week 1)

**Goal:** Understand the fundamental concepts of computer networking and learn how devices communicate over the Internet.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Explain what a computer network is.
- Understand the purpose of IP addresses and MAC addresses.
- Explain how DHCP assigns IP addresses.
- Understand how DNS translates domain names into IP addresses.
- Describe the OSI Model and the responsibility of each layer.
- Use basic Linux networking commands.
- Explain what happens behind the scenes when visiting a website.
- Build a simple network diagram.

---

# Before We Start

Every day, we perform actions like:

- Opening Google
- Watching YouTube
- Sending emails
- Using Facebook
- Playing online games

Although these actions seem simple, they involve dozens of networking technologies working together.

When you type:

```
https://www.google.com
```

your computer doesn't magically know where Google is.

It must first discover:

- Where Google is located
- Which route to take
- Which protocol to use
- How to establish a connection
- How to securely exchange data

Understanding this process is one of the most important skills in cybersecurity.

---

# What is a Computer Network?

A **computer network** is a collection of devices connected together so they can exchange information.

A network may include:

- Computers
- Mobile phones
- Servers
- Printers
- Routers
- Switches
- Firewalls

Example:

```
Laptop
    │
Wi-Fi Router
    │
Internet
    │
Google Server
```

Every message you send travels through multiple networking devices before reaching its destination.

---

# Real-Life Analogy

Imagine sending a letter to your friend.

You need:

- Your friend's address
- A postal office
- A delivery route
- A mailbox

Computer networks work similarly.

| Real Life | Networking |
|------------|------------|
| House | Computer |
| Home Address | IP Address |
| Postal Service | Internet |
| Mail Carrier | Router |
| Address Book | DNS |
| Letter | Data Packet |

---

# What is an IP Address?

An **IP (Internet Protocol) Address** is a unique address assigned to every device on a network.

Think of it as your home's street address.

Without an IP address, no device would know where to send data.

Example IPv4 address

```
192.168.1.15
```

Another example

```
8.8.8.8
```

(Google Public DNS)

---

## Private vs Public IP

### Private IP

Used inside your local network.

Examples

```
192.168.x.x

10.x.x.x

172.16.x.x – 172.31.x.x
```

These addresses are **not accessible directly from the Internet**.

---

### Public IP

Assigned by your Internet Service Provider (ISP).

This is how the Internet identifies your network.

Example

```
103.145.112.45
```

---

# What Happens Internally?

When your laptop joins Wi-Fi,

it asks:

> "Can someone give me an IP address?"

The router replies with an available address.

Now your laptop has an identity on the network.

---

# What is a MAC Address?

Every network interface card (NIC) has a **MAC Address**.

MAC stands for

```
Media Access Control
```

Unlike IP addresses,

MAC addresses are generally assigned by the manufacturer.

Example

```
08:00:27:12:34:56
```

Think of it as your device's fingerprint.

Even if your IP changes,

your MAC address usually remains the same.

---

# IP Address vs MAC Address

| IP Address | MAC Address |
|-------------|-------------|
| Logical Address | Physical Address |
| Can change | Usually permanent |
| Used across networks | Used inside local network |
| Assigned by router/DHCP | Assigned by manufacturer |

---

# DHCP (Dynamic Host Configuration Protocol)

## Why Do We Need DHCP?

Imagine a university with 500 students.

If every student had to manually configure:

- IP Address
- Gateway
- DNS Server

network management would become impossible.

DHCP automates this process.

---

## How DHCP Works

When your laptop connects to Wi-Fi:

```
Laptop

↓

DHCP Discover

↓

Router

↓

DHCP Offer

↓

Laptop

↓

DHCP Request

↓

Router

↓

DHCP Acknowledgement
```

Now your computer automatically receives:

- IP Address
- Gateway
- DNS Server
- Subnet Mask

---

# DNS (Domain Name System)

Humans remember

```
google.com
```

Computers remember

```
142.250.193.14
```

DNS converts domain names into IP addresses.

Think of DNS as the Internet's phonebook.

---

## Example

You type

```
google.com
```

DNS replies

```
142.250.xx.xx
```

Now your browser knows where to send requests.

---

# OSI Model

The **OSI (Open Systems Interconnection) Model** describes how data moves across a network.

```
Application
Presentation
Session
Transport
Network
Data Link
Physical
```

---

## Layer 7 — Application

Responsible for user applications.

Examples

- HTTP
- HTTPS
- FTP
- SMTP
- DNS

---

## Layer 6 — Presentation

Responsible for

- Encryption
- Compression
- Data formatting

Example

HTTPS encryption occurs here.

---

## Layer 5 — Session

Responsible for

Creating

Maintaining

Closing communication sessions.

---

## Layer 4 — Transport

Responsible for reliable communication.

Protocols

- TCP
- UDP

TCP ensures data arrives correctly.

---

## Layer 3 — Network

Responsible for routing packets.

Uses

IP Addresses

Routers operate here.

---

## Layer 2 — Data Link

Responsible for communication inside the local network.

Uses

MAC Addresses

Switches operate here.

---

## Layer 1 — Physical

Responsible for transmitting bits.

Examples

- Ethernet Cable
- Fiber Optic
- Wi-Fi Signals

---

# Easy Way to Remember

```
All

People

Seem

To

Need

Data

Processing
```

---

# Lab Activity

## Objective

Explore your own network configuration using Linux networking commands.

---

# Command 1 — ip a

## Purpose

Displays all network interfaces.

---

## Command

```bash
ip a
```

---

## What Happens Internally?

Linux asks the kernel:

> "Show me every network interface currently available."

It displays:

- Interface name
- MAC address
- IP address
- Interface status

---

## Example Output

```bash
eth0

inet 192.168.1.15/24
```

---

## What to Observe

- Interface name
- IPv4 Address
- MAC Address
- UP/DOWN state

---

# Command 2 — ip route

## Purpose

Displays the routing table.

---

## Command

```bash
ip route
```

---

## What Happens Internally?

Linux checks its routing table.

This tells Linux where packets should be sent.

Example

```
Destination

↓

Gateway

↓

Network Interface
```

---

## Example Output

```bash
default via 192.168.1.1 dev eth0
```

Meaning

Your router's IP is

```
192.168.1.1
```

All Internet traffic goes there first.

---

# Command 3 — cat /etc/resolv.conf

## Purpose

Shows which DNS server your computer uses.

---

## Command

```bash
cat /etc/resolv.conf
```

---

## Example Output

```bash
nameserver 8.8.8.8
```

Meaning

Your computer asks Google's DNS server to resolve domain names.

---

# Command 4 — dig google.com

## Purpose

Queries the DNS server directly.

---

## Command

```bash
dig google.com
```

---

## What Happens Internally?

Your computer sends a DNS request asking

> "What is the IP address of google.com?"

The DNS server replies with Google's IP.

---

## Observe

- ANSWER SECTION
- Query Time
- Server Used
- Returned IP

---

# Command 5 — nslookup google.com

## Purpose

Another DNS lookup tool.

---

## Command

```bash
nslookup google.com
```

Compare its output with `dig`.

---

# Command 6 — ping

## Purpose

Tests connectivity.

---

## Command

```bash
ping -c 4 google.com
```

---

## What Happens Internally?

Your computer sends **ICMP Echo Requests**.

Google replies with **ICMP Echo Replies**.

---

## Observe

- Response Time
- Packet Loss
- Average Latency

---

# Command 7 — traceroute

## Purpose

Shows every router your packets travel through.

---

## Command

```bash
traceroute google.com
```

---

## What Happens Internally?

Linux sends packets with gradually increasing **TTL (Time To Live)** values.

Each router decreases the TTL by 1.

When TTL reaches zero,

the router responds,

allowing Linux to discover every hop.

---

## Observe

- Number of hops
- ISP routers
- Average latency

---

# Complete Journey of Opening Google

When you type

```
https://www.google.com
```

this is what actually happens.

## Step 1

You enter

```
google.com
```

into your browser.

---

## Step 2

Browser checks its cache.

If the IP is already known,

it skips DNS.

Otherwise,

it asks the DNS server.

---

## Step 3

DNS replies

```
google.com

↓

142.xxx.xxx.xxx
```

---

## Step 4

Your computer checks

```
Routing Table
```

using

```bash
ip route
```

to determine the best path.

---

## Step 5

Your packet is sent to

```
Router

↓

ISP

↓

Internet
```

---

## Step 6

A **TCP Three-Way Handshake** establishes a reliable connection.

```
SYN

↓

SYN-ACK

↓

ACK
```

---

## Step 7

Browser sends an HTTPS request.

```
GET /
```

---

## Step 8

Google responds with

- HTML
- CSS
- JavaScript
- Images

---

## Step 9

The browser downloads these resources.

---

## Step 10

Finally,

the browser renders the webpage on your screen.

---

# Assignment Questions

Answer the following in your own words.

1. What is a network?

2. Difference between IP and MAC Address?

3. Why is DHCP important?

4. Why do we need DNS?

5. What is the purpose of the OSI Model?

6. Explain what happens after typing **google.com** into your browser.

7. What is the difference between `dig` and `nslookup`?

8. What does `traceroute` show?

---

# Draw.io Diagram

Create a network diagram similar to this.

```
+-----------+
| Your Laptop |
+-----------+
      │
      ▼
+-----------+
| Wi-Fi Router |
+-----------+
      │
      ▼
+-----------+
| ISP Network |
+-----------+
      │
      ▼
+-----------+
| DNS Server |
+-----------+
      │
      ▼
+----------------+
| Google Server  |
+----------------+
      │
      ▼
Response Returns
Back to Your Laptop
```

---

# Screenshots to Include

- `ip a`
- `ip route`
- `cat /etc/resolv.conf`
- `dig google.com`
- `nslookup google.com`
- `ping -c 4 google.com`
- `traceroute google.com`
- Draw.io Network Diagram

---

# Interview Questions

1. What is the difference between an IP address and a MAC address?

2. Explain the DHCP process.

3. What is DNS and why is it necessary?

4. Which OSI layer uses IP addresses?

5. Which OSI layer uses MAC addresses?

6. Explain the TCP Three-Way Handshake.

7. What does `ping` actually test?

8. What is the purpose of `traceroute`?

---

# Key Takeaways

- A network allows devices to communicate and exchange data.
- Every device requires an IP address to communicate over a network.
- Every network interface has a unique MAC address used within the local network.
- DHCP automatically assigns network configuration information, reducing manual setup.
- DNS translates human-readable domain names into IP addresses.
- The OSI Model provides a structured way to understand how data travels across a network.
- Linux networking commands help inspect interfaces, routes, DNS configuration, connectivity, and packet paths.
- Visiting a website involves DNS resolution, routing, TCP connection establishment, HTTP/HTTPS communication, and browser rendering.

---

# Deliverables

- ✅ Completed all networking commands and documented their outputs.
- ✅ Answered the networking reflection questions.
- ✅ Created `networking-notes.md`.
- ✅ Included screenshots of each networking command.
- ✅ Designed and added a Draw.io (or hand-drawn) network communication diagram.
- ✅ Understood the complete journey of a web request from browser to server and back.
````
