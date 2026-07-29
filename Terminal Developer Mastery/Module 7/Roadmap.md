Excellent. This is **Module 7**, and it is one of the most important modules for becoming a strong backend engineer.

After Linux, Shell, Docker, CLI tools, Neovim, Git, and SSH, you're now ready to understand **how data actually travels across the Internet**.

---

# Module 7 — Networking for Backend Engineers ⭐⭐⭐⭐⭐

> Learn how computers communicate over networks, how web requests travel, and how to debug networking problems like an experienced backend engineer.

**Difficulty:** Intermediate → Advanced

**Goal:**

By the end of this module, you'll be able to troubleshoot servers, debug API issues, understand HTTP deeply, configure reverse proxies, and diagnose networking problems confidently.

---

# Module Structure (15 Lessons)

## Part 1 — Networking Fundamentals

### Lesson 1

**How the Internet Actually Works**

Learn:

- LAN vs WAN
- Internet
- ISP
- Routers
- Switches
- Modems
- Public vs Private networks

You'll finally understand what happens when someone types:

```
<https://google.com>
```

---

### Lesson 2

**The TCP/IP Stack**

Understand the four layers:

```
Application
Transport
Internet
Link
```

Also compare it with the OSI Model.

---

### Lesson 3

**IP Addresses**

Learn:

- IPv4
- IPv6
- Public IP
- Private IP
- Loopback
- Broadcast
- Gateway

Commands:

```
ip addr
hostname -I
curl ifconfig.me
```

---

### Lesson 4

**Subnetting**

Understand:

- CIDR
- /24
- /16
- /8
- Network IDs
- Host IDs

Example:

```
192.168.1.0/24
```

This lesson removes the fear of subnet masks.

---

### Lesson 5

**Routing**

Understand:

```
How packets find their destination
```

Commands:

```
ip route

traceroute

tracepath
```

---

## Part 2 — DNS

### Lesson 6

DNS in depth

Learn:

- A record
- AAAA
- CNAME
- MX
- TXT
- NS
- TTL

Commands:

```
dig

host

nslookup
```

---

### Lesson 7

DNS Resolution Process

You'll follow a request from

```
google.com
```

to its IP step by step.

---

## Part 3 — Linux Networking

### Lesson 8

Interfaces

Commands:

```
ip

ifconfig

nmcli
```

Understand:

- Ethernet
- Wi-Fi
- Virtual interfaces
- Bridges

---

### Lesson 9

Socket Inspection

Master:

```
ss
```

Examples:

```
ss -tuln

ss -tp

ss -s
```

This is one of the most-used debugging tools on Linux.

---

### Lesson 10

Network Namespaces

Learn how Docker isolates networking.

Commands:

```
ip netns

veth

bridge
```

This explains how containers communicate.

---

## Part 4 — Firewalls

### Lesson 11

iptables

Learn:

- Chains
- Tables
- Rules
- ACCEPT
- DROP

---

### Lesson 12

nftables

Modern replacement for iptables.

You'll learn:

```
nft list ruleset
```

and create simple firewall rules.

---

## Part 5 — Network Debugging

### Lesson 13

tcpdump

Capture packets.

Examples:

```
tcpdump

tcpdump port 80

tcpdump host google.com
```

You'll literally see packets moving.

---

### Lesson 14

HTTP + HTTPS + TLS

Understand:

- HTTP request lifecycle
- HTTPS
- TLS handshake
- Certificates
- Ports
- Keep-alive
- HTTP/1.1
- HTTP/2
- HTTP/3 (overview)

This lesson is extremely valuable for backend interviews.

---

### Lesson 15

Reverse Proxies & Load Balancers

Learn:

- Reverse Proxy
- Forward Proxy
- Nginx
- Load Balancer
- Round Robin
- Health Checks
- Sticky Sessions
- SSL Termination

This ties together networking with backend deployment.

---

# Tools You'll Master

- `ip`
- `ss`
- `ping`
- `traceroute`
- `tracepath`
- `dig`
- `host`
- `nslookup`
- `tcpdump`
- `iptables`
- `nft`
- `curl`
- `wget`
- `netcat (nc)`
- `openssl`
- `nginx`

---

# Practical Labs

By the end of the module, you'll be able to:

- Build your own mini network using namespaces.
- Capture packets with `tcpdump`.
- Debug why an API is unreachable.
- Diagnose DNS failures.
- Inspect listening ports with `ss`.
- Create firewall rules with `nftables`.
- Configure an Nginx reverse proxy.
- Trace the route packets take to a server.
- Understand how Docker networking works internally.
- Debug common HTTPS and TLS issues.

---

# What You'll Be Able to Explain in an Interview

- How a browser reaches a website from a URL.
- The difference between TCP and UDP.
- Why DNS caching improves performance.
- How routing tables determine packet paths.
- Why HTTPS is more secure than HTTP.
- How a reverse proxy differs from a load balancer.
- How Docker containers communicate on the same host.
- How to identify which process is listening on a port.
- How to investigate packet loss or connection failures.

---

# After This Module

Once you complete Networking, the next logical modules are:

- **Module 8 — Nginx & Web Servers**
- **Module 9 — Observability (Logging, Monitoring & Metrics)**
- **Module 10 — Linux Security & Hardening**
- **Module 11 — System Design Fundamentals**
- **Module 12 — CI/CD & Deployment Pipelines**

Networking is one of the core skills that separates a developer who can write code from an engineer who can diagnose production issues. Mastering this module will make you much more effective in backend development, DevOps, and cloud environments.

Let's begin with **Lesson 1: How the Internet Actually Works** in the next step.