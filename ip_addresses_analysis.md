# 🧠 IP Addresses & Analysis

## 📘 What Is an IP Address?

An **IP address** (Internet Protocol address) is a numerical label assigned to each device connected to a network that uses the Internet Protocol to communicate. It acts like a *mailing address* for your computer.

There are two types:
- **IPv4** (what we usually deal with): `192.168.0.1`
- **IPv6** (not your problem yet): `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

Each IPv4 address is 32 bits, split into four *octets* (0-255), like:  
`192.168.1.1`

There are two kinds of IP addresses:
- **Public:** Routable on the internet (e.g., Google DNS: `8.8.8.8`)
- **Private:** Used in internal networks. Non-routable.

---

## 🔐 Common IP Ranges & What They Mean

| CIDR | Range | Purpose | Explanation |
|------|-------|---------|-------------|
| `10.0.0.0/8` | `10.0.0.0` - `10.255.255.255` | Private Network | Often used in enterprise LANs |
| `172.16.0.0/12` | `172.16.0.0` - `172.31.255.255` | Private Network | Less common, but used in VPNs, cloud |
| `192.168.0.0/16` | `192.168.0.0` - `192.168.255.255` | Private Network | Most home routers use this |
| `127.0.0.0/8` | `127.0.0.0` - `127.255.255.255` | Loopback | Refers to *your own machine* |
| `169.254.0.0/16` | `169.254.0.0` - `169.254.255.255` | Link-local | Automatic IP when DHCP fails |
| `0.0.0.0/8` | `0.0.0.0` - `0.255.255.255` | "This network" | Used to refer to all local addresses |
| `224.0.0.0/4` | `224.0.0.0` - `239.255.255.255` | Multicast | For sending packets to multiple hosts |
| `8.8.8.8` | Single IP | Google DNS | Just an example of a public IP |

---

## 🔍 IP Address Lookup Tools

Use these to check IP reputation, geolocation, services exposed, and more.

| Tool | Link | What It Does |
|------|------|--------------|
| **AbuseIPDB** | [https://www.abuseipdb.com/](https://www.abuseipdb.com/) | Crowdsourced IP reputation and abuse reports |
| **Cisco Talos Intelligence** | [https://talosintelligence.com/](https://talosintelligence.com/) | Threat intelligence on IPs/domains, shows history of malicious activity |
| **VirusTotal** | [https://www.virustotal.com/](https://www.virustotal.com/) | Aggregates threat engine results for IPs, URLs, files |
| **IPVoid** | [https://www.ipvoid.com/](https://www.ipvoid.com/) | DNSBL checks, IP reputation, hostname lookup |
| **Shodan** | [https://www.shodan.io/](https://www.shodan.io/) | Scans the internet for open ports/services on an IP |

---

## 📁 IP Analysis Log Template

Use this to keep track of IPs you’ve looked up. Fill in each section like a cyber-squirrel hoarding acorns.

```markdown
## 🔎 IP: [insert IP here]

**Date:** YYYY-MM-DD  
**Context:** Found in [SIEM alert / TryHackMe / CTF / Threat Intel]

### 🌐 Lookups:

- **AbuseIPDB:** [link] — Reputation: 80/100 — Flags: SSH brute force
- **Cisco Talos:** [link] — Malicious category: Malware Hosting
- **VirusTotal:** [link] — Flagged by 7/90 engines
- **Shodan:** [link] — Open ports: 80 (nginx), 22 (SSH), 443 (self-signed cert)

### 📍 Summary:
This IP was used in a simulated phishing payload. It has a history of brute force SSH attempts and currently exposes a default nginx server. Low confidence in real-world impact, but decent training example.

