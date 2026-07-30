The next module after **Module 8 — Nginx & Web Servers** is:

# Module 9 — Observability (Logging, Monitoring & Metrics) ⭐⭐⭐⭐⭐

> Learn how to monitor Linux servers and backend applications, collect logs, track metrics, set up alerts, and troubleshoot production issues like an SRE or backend engineer.

**Difficulty:** Intermediate → Advanced

**Goal:** By the end of this module, you'll be able to detect problems before users report them, analyze logs, monitor application health, and build a complete observability stack.

---

# Part 1 — Observability Fundamentals

## Lesson 1: What is Observability?

- Monitoring vs Observability
- Logs
- Metrics
- Traces
- Why observability matters
- The three pillars of observability

---

## Lesson 2: Linux Logs

- Log files
- `/var/log`
- Common system logs
- Viewing logs
- Searching logs
- Understanding log formats

---

## Lesson 3: systemd Journal

- `journalctl`
- Filtering logs
- Service logs
- Boot logs
- Following live logs
- Persistent journals

---

## Lesson 4: Log Management

- Log rotation
- `logrotate`
- Retention policies
- Compression
- Cleaning old logs
- Best practices

---

# Part 2 — Application Logging

## Lesson 5: Logging in Backend Applications

- Structured logging
- Log levels
- JSON logs
- Correlation IDs
- Request IDs
- Error logging

---

## Lesson 6: Logging Best Practices

- What to log
- What not to log
- Sensitive data
- Performance impact
- Log sampling
- Production logging guidelines

---

## Lesson 7: Centralized Logging

- Why centralize logs?
- Log aggregation
- Log shipping
- Log pipelines
- Introduction to the ELK Stack
- Introduction to Loki

---

# Part 3 — Monitoring

## Lesson 8: Monitoring Basics

- System health
- CPU
- Memory
- Disk
- Network
- Uptime

---

## Lesson 9: Linux Monitoring Tools

- `top`
- `htop`
- `btop`
- `vmstat`
- `iostat`
- `free`
- `uptime`
- `sar`

---

## Lesson 10: Monitoring Processes

- `ps`
- `pgrep`
- `pidof`
- `pstree`
- Process states
- Zombie processes

---

## Lesson 11: Disk Monitoring

- `df`
- `du`
- Disk usage
- Inodes
- I/O bottlenecks
- Storage health

---

## Lesson 12: Network Monitoring

- `ss`
- `ip`
- `iftop`
- `nload`
- `tcpdump`
- Network statistics
- Connection monitoring

---

# Part 4 — Metrics

## Lesson 13: Prometheus Fundamentals

- What are metrics?
- Prometheus architecture
- Exporters
- Time-series data
- Scraping
- Labels

---

## Lesson 14: Grafana Dashboards

- Installing Grafana
- Data sources
- Dashboard creation
- Panels
- Variables
- Visualizations

---

## Lesson 15: Node Exporter

- Installing Node Exporter
- System metrics
- CPU metrics
- Memory metrics
- Filesystem metrics
- Network metrics

---

# Part 5 — Alerting

## Lesson 16: Alerting Basics

- Why alerts matter
- Thresholds
- Alert fatigue
- Alert priorities
- Escalation

---

## Lesson 17: Prometheus Alertmanager

- Alert rules
- Alertmanager
- Email alerts
- Slack alerts
- Routing alerts
- Silencing alerts

---

# Part 6 — Performance Analysis

## Lesson 18: Finding Performance Bottlenecks

- High CPU
- Memory leaks
- Disk bottlenecks
- Network latency
- Slow applications
- Root cause analysis

---

## Lesson 19: Production Incident Debugging

- Troubleshooting methodology
- Reading logs
- Checking services
- Network verification
- Resource analysis
- Building an incident timeline
- Postmortems

---

# Part 7 — Real-World Observability

## Lesson 20: Complete Monitoring Stack Project

Build a production-ready monitoring environment that includes:

- Linux server monitoring
- Application logging
- Prometheus
- Grafana dashboards
- Node Exporter
- Centralized logging
- Alertmanager
- Email/Slack alerts
- Performance dashboards
- Incident troubleshooting workflow

---

# Tools You'll Master

- `journalctl`
- `logrotate`
- `top`
- `htop`
- `btop`
- `vmstat`
- `iostat`
- `sar`
- `free`
- `df`
- `du`
- `ps`
- `pgrep`
- `pstree`
- `ss`
- `iftop`
- `nload`
- `tcpdump`
- Prometheus
- Grafana
- Node Exporter
- Alertmanager
- Loki
- ELK Stack (overview)

---

# Mini Projects

1. Analyze Linux system logs to diagnose a failed service.
2. Configure automatic log rotation for a custom application.
3. Build a JSON-based logging system for a backend API.
4. Set up Prometheus to collect system metrics.
5. Create Grafana dashboards for CPU, memory, disk, and network.
6. Configure Node Exporter to monitor a Linux server.
7. Create alerts for high CPU, low disk space, and service failures.
8. Investigate a simulated production outage using logs and metrics.
9. Build a basic centralized logging pipeline.
10. Deploy a complete observability stack using Docker Compose.

---

# What You'll Be Able to Explain in Interviews

- The difference between logs, metrics, and traces.
- How to investigate a production incident.
- Why structured logging is important.
- How Prometheus collects metrics.
- How Grafana visualizes data.
- How alerting systems reduce downtime.
- How to identify CPU, memory, disk, or network bottlenecks.
- How observability supports reliable backend systems.
- How to build a monitoring solution for production servers.

After completing this module, you'll have the skills to monitor and troubleshoot backend applications and Linux servers effectively. The next step is **Module 10 — Linux Security & Hardening**, where you'll learn to secure production systems against common threats.