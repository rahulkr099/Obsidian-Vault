# Module 8 — Nginx & Web Servers ⭐⭐⭐⭐⭐

> Learn how web servers work, how Nginx serves websites and APIs, and how it is used in real production environments.

**Difficulty:** Intermediate → Advanced

**Goal:** By the end of this module, you'll be able to deploy backend applications with Nginx, configure reverse proxies, optimize performance, secure web traffic with HTTPS, and troubleshoot common web server issues.

---

# Part 1 — Web Server Fundamentals

## Lesson 1: What is a Web Server?

- What is a web server?
- Static vs Dynamic content
- Client-Server model
- Request-Response lifecycle
- Popular web servers
- Where Nginx fits

---

## Lesson 2: Installing and Exploring Nginx

- Installing Nginx
- Starting and stopping Nginx
- Service management with `systemctl`
- Directory structure
- Configuration files
- Testing configuration

---

## Lesson 3: How Nginx Processes Requests

- Master process
- Worker processes
- Event-driven architecture
- Connection handling
- Worker connections
- Performance model

---

## Lesson 4: Nginx Configuration Basics

- `nginx.conf`
- Include files
- Contexts
- Directives
- Blocks
- Configuration hierarchy
- Best practices

---

## Lesson 5: Serving Static Files

- HTML
- CSS
- JavaScript
- Images
- Downloads
- Directory indexing
- Cache headers

---

# Part 2 — Virtual Hosts

## Lesson 6: Server Blocks

- Virtual Hosts
- Multiple websites
- Default server
- Host matching
- Server names
- Listening ports

---

## Lesson 7: Location Blocks

- Prefix matching
- Exact matching
- Regex matching
- Location priority
- URI handling
- Nested locations

---

## Lesson 8: URL Rewriting & Redirects

- 301 Redirect
- 302 Redirect
- Rewrite rules
- Permanent redirects
- Temporary redirects
- Pretty URLs

---

# Part 3 — Reverse Proxy

## Lesson 9: Reverse Proxy Fundamentals

- What is a reverse proxy?
- Benefits
- Proxy architecture
- Backend communication
- Request forwarding

---

## Lesson 10: Reverse Proxy for Backend Apps

- Node.js
- Express
- Django
- Flask
- Spring Boot
- [ASP.NET](http://ASP.NET)
- Multiple backend services

---

## Lesson 11: Proxy Headers

- X-Forwarded-For
- X-Forwarded-Proto
- Host header
- Client IP
- Forwarded headers
- Trust proxy

---

# Part 4 — Load Balancing

## Lesson 12: Load Balancing

- Upstream blocks
- Round Robin
- Least Connections
- IP Hash
- Weighted balancing
- Health checks
- Failover

---

## Lesson 13: Scaling Applications

- Horizontal scaling
- Multiple backend servers
- High availability
- Zero downtime
- Rolling updates
- Blue-Green deployment overview

---

# Part 5 — HTTPS & Security

## Lesson 14: SSL/TLS Certificates

- SSL vs TLS
- Certificate types
- Certificate chain
- Self-signed certificates
- CA-issued certificates
- Let's Encrypt overview

---

## Lesson 15: HTTPS Configuration

- Enable HTTPS
- Force HTTPS
- HTTP to HTTPS redirect
- HSTS
- Secure ciphers
- TLS versions

---

## Lesson 16: Security Hardening

- Hide Nginx version
- Security headers
- Rate limiting
- Basic authentication
- IP allow/deny
- Prevent directory traversal

---

# Part 6 — Performance Optimization

## Lesson 17: Caching

- Browser cache
- Proxy cache
- FastCGI cache
- Cache-Control
- Expires headers
- Cache invalidation

---

## Lesson 18: Compression & Performance

- Gzip
- Brotli
- Keep-Alive
- Buffer tuning
- Worker tuning
- File descriptor limits
- Benchmarking basics

---

# Part 7 — Logging & Monitoring

## Lesson 19: Logs and Debugging

- Access logs
- Error logs
- Custom log formats
- Log rotation
- Debug logging
- Troubleshooting common errors

---

## Lesson 20: Production Deployment Project

Build a complete production-ready Nginx setup that includes:

- Hosting a static website
- Reverse proxy for a backend API
- Multiple virtual hosts
- HTTPS with TLS
- Load balancing between backend servers
- Rate limiting
- Security headers
- Compression
- Caching
- Log analysis
- Performance tuning
- Zero-downtime configuration reloads

---

# Commands You'll Master

- `nginx`
- `nginx -t`
- `nginx -T`
- `systemctl start nginx`
- `systemctl stop nginx`
- `systemctl restart nginx`
- `systemctl reload nginx`
- `journalctl -u nginx`
- `curl`
- `openssl`
- `ab` (ApacheBench)
- `wrk` (HTTP benchmarking)
- `ss`
- `tcpdump`

---

# Mini Projects

1. Host a static portfolio website with Nginx.
2. Reverse proxy a Node.js/Express application.
3. Serve multiple websites from one server using virtual hosts.
4. Secure a website with HTTPS.
5. Configure load balancing across multiple backend instances.
6. Enable caching and compression for faster responses.
7. Protect an API with rate limiting and security headers.
8. Analyze logs to identify errors and performance bottlenecks.
9. Perform a zero-downtime Nginx configuration reload.
10. Deploy a production-ready web server from scratch.

---

# What You'll Be Able to Explain in Interviews

- How Nginx differs from Apache.
- Why Nginx is event-driven and highly scalable.
- How a reverse proxy works.
- How load balancing distributes traffic.
- How HTTPS is configured in Nginx.
- How to optimize Nginx for high traffic.
- How caching improves website performance.
- How to troubleshoot common Nginx errors.
- How Nginx fits into a modern backend architecture with Docker and cloud deployments.

This module prepares you to confidently deploy and manage web applications in production and serves as a strong foundation for the next topics: **Observability, Linux Security, System Design, and CI/CD**.