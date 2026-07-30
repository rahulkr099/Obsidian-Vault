# Module 5 — Networking Deep Dive for Backend Engineers 🌐

> **Goal:** Understand _how data travels from a user's browser to your backend and back again._

After this module, concepts like **HTTP, HTTPS, TCP, DNS, WebSockets, Reverse Proxies, Load Balancers, APIs, and Microservices** will make much more sense because you'll understand what happens under the hood.

---

# 📚 Module Overview

|Lesson|Topic|Difficulty|Priority|
|---|---|---|---|
|1|Networking Fundamentals|⭐⭐⭐|⭐⭐⭐⭐⭐|
|2|TCP/IP Deep Dive|⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|3|DNS Deep Dive|⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|4|HTTP & HTTPS Internals|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|5|REST APIs & HTTP Methods|⭐⭐⭐|⭐⭐⭐⭐⭐|
|6|WebSockets & Real-Time Communication|⭐⭐⭐⭐|⭐⭐⭐⭐|
|7|Reverse Proxy & Load Balancing|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|8|TLS/SSL & Certificates|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|9|CORS, Cookies & Sessions|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|10|API Security|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|11|Performance & Caching|⭐⭐⭐⭐⭐|⭐⭐⭐⭐|
|12|Networking Tools & Debugging|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|
|13|Networking Capstone Project|⭐⭐⭐⭐⭐|⭐⭐⭐⭐⭐|

---

# 🎯 What You'll Build

Throughout this module you'll build and debug a production-like networking setup:

```
                 Internet
                      │
                      ▼
             DNS (example.com)
                      │
                      ▼
               Public IP Address
                      │
                      ▼
            Firewall (UFW/Security Group)
                      │
                      ▼
          Nginx Reverse Proxy (HTTPS)
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
    Backend API              Static Frontend
   (Node.js:5000)             (React Build)
          │
          ▼
      MongoDB Atlas
```

By the end of the module, you'll understand every arrow in this diagram.

---

# 🧠 Skills You'll Gain

You'll be able to explain:

- How browsers connect to servers
- How DNS works
- Why HTTPS is secure
- How REST APIs communicate
- Why CORS exists
- Why cookies sometimes disappear
- How JWT authentication travels
- How WebSockets stay connected
- How Nginx forwards requests
- How load balancers distribute traffic
- Why APIs become slow
- How CDNs improve speed

---

# 🛠 Tools You'll Learn

## Network Utilities

- `ping`
- `curl`
- `wget`
- `doggo`
- `ss`
- `nc` (Netcat)
- `traceroute`
- `tracepath`

---

## Debugging

- Chrome DevTools → Network Tab
- Postman
- Bruno
- `curl`
- Nginx logs
- Browser headers

---

## Backend

- Express
- Axios
- Fetch API
- WebSocket
- [Socket.IO](http://Socket.IO) (concepts)
- Nginx

---

# 📖 Lesson Breakdown

---

# Lesson 1 — Networking Fundamentals

You'll learn:

- What is a network?
- Client vs Server
- LAN vs WAN
- Internet architecture
- Packets
- Routers
- Switches
- Ports
- IP addresses
- Request-response lifecycle

Mini project:

Build your own network diagram.

---

# Lesson 2 — TCP/IP Deep Dive

You'll learn:

- TCP
- UDP
- Reliability
- Three-way handshake
- Four-way termination
- Packet retransmission
- Flow control
- Congestion control
- MTU

You'll understand why TCP is used for:

- HTTP
- HTTPS
- SSH
- MongoDB

---

# Lesson 3 — DNS Deep Dive

You'll learn:

- Domain names
- Recursive resolver
- Root servers
- TLD servers
- Authoritative servers
- A record
- AAAA
- CNAME
- MX
- TXT
- TTL

Mini project:

Trace how `google.com` resolves to an IP.

---

# Lesson 4 — HTTP & HTTPS Internals

Probably the most important lesson.

You'll learn:

- HTTP request
- HTTP response
- Headers
- Status codes
- Cookies
- Keep-alive
- HTTP/2
- HTTP/3
- HTTPS
- TLS handshake

You'll manually inspect requests using `curl`.

---

# Lesson 5 — REST APIs

Topics:

- GET
- POST
- PUT
- PATCH
- DELETE
- Idempotency
- Resources
- JSON
- Status codes
- API versioning

---

# Lesson 6 — WebSockets

Learn:

- Why polling is inefficient
- Persistent connections
- Handshake
- Frames
- Real-time communication

Applications:

- Chat
- Games
- Stock prices
- Notifications

---

# Lesson 7 — Reverse Proxy

Topics:

- Nginx
- Proxying
- Static serving
- SSL termination
- Compression
- Rate limiting
- Load balancing

You'll configure Nginx.

---

# Lesson 8 — TLS & Certificates

Topics:

- Encryption
- Public keys
- Private keys
- Certificates
- Certificate Authorities
- Let's Encrypt
- Certbot
- HTTPS verification

---

# Lesson 9 — CORS & Cookies

Probably the most misunderstood backend topic.

You'll learn:

- Same Origin Policy
- CORS
- Preflight requests
- OPTIONS
- Credentials
- Cookies
- SameSite
- HttpOnly
- Secure
- JWT storage

This lesson will directly address the CORS and cookie issues you encountered while deploying your projects.

---

# Lesson 10 — API Security

Topics:

- JWT
- OAuth
- API Keys
- Rate limiting
- Helmet
- CSRF
- XSS
- SQL Injection
- NoSQL Injection

---

# Lesson 11 — Performance & Caching

Learn:

- Browser cache
- CDN
- Redis
- Cache-Control
- ETags
- Compression
- Gzip
- Brotli

---

# Lesson 12 — Networking Tools

Practice using:

```bash
curl
doggo
ping
ss
nc
traceroute
tcpdump (introduction)
```

You'll debug:

- DNS failures
- Slow APIs
- SSL issues
- Port conflicts
- Connection refusals

---

# Lesson 13 — Networking Capstone

You'll deploy a complete production backend with:

```
User
 │
 ▼
DNS
 │
 ▼
HTTPS
 │
 ▼
Nginx
 │
 ▼
Express
 │
 ▼
MongoDB
```

Then you'll troubleshoot deliberately introduced networking failures such as:

- DNS misconfiguration
- CORS errors
- SSL certificate problems
- Reverse proxy mistakes
- Backend port conflicts
- 502 Bad Gateway
- 504 Gateway Timeout
- Connection refused

---

# 🎯 Learning Outcomes

After Module 5, you'll be able to answer questions like:

- Why does `localhost` work but my deployed API doesn't?
- Why does my React app show a CORS error?
- Why do cookies disappear after deployment?
- Why is HTTPS required for secure cookies?
- Why does Nginx return **502 Bad Gateway**?
- What happens after typing `https://google.com` into a browser?
- How does a JWT travel from the server to the client?
- Why are some APIs fast and others slow?
- How does a browser reuse a TCP connection?

---

# 🏆 Module 5 Challenge

At the end of this module, you'll complete a production networking challenge where you'll:

- Deploy a Node.js backend behind Nginx
- Secure it with HTTPS
- Configure DNS
- Fix CORS issues
- Implement JWT authentication
- Test with `curl` and browser developer tools
- Simulate and resolve common production networking failures

---

# ⭐ Roadmap Progress

```
✅ Module 1 — Shell Scripting
✅ Module 2 — Linux Command Line Essentials
✅ Module 3 — Bash & Advanced Shell Tools
✅ Module 4 — Linux System Administration

🟨 Module 5 — Networking Deep Dive (Current)

⬜ Module 6 — Docker
⬜ Module 7 — Docker Compose
⬜ Module 8 — Reverse Proxy (Advanced Nginx)
⬜ Module 9 — CI/CD
⬜ Module 10 — Cloud & VPS
⬜ Module 11 — Kubernetes Fundamentals
⬜ Module 12 — Production DevOps Project
```

---

# 💡 Why This Module Matters

Networking is one of the biggest differentiators between a junior and a mid-level backend engineer.

Many developers can build an Express API, but far fewer can confidently explain why it fails in production or trace a request across DNS, TCP, HTTPS, Nginx, the application, and the database.

Mastering this module will help you troubleshoot deployments faster, design more reliable systems, and communicate effectively during backend interviews and production incidents.

## 📖 Next Lesson

**Lesson 1 – Networking Fundamentals**

You'll begin with the core concepts of networking, including clients, servers, IP addresses, ports, packets, LAN vs. WAN, and the complete journey of a request from a browser to your backend server.