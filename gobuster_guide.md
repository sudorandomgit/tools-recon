# Gobuster Recon Use Case Guide

> A short guide explaining *when* to use each mode in Gobuster with real-world context. Less syntax, more sense.

---

## 🤖 What is Gobuster?

Gobuster is a tool used to brute-force discoverable content on a target: hidden directories, files, subdomains, virtual hosts, and more. It's noisy, blunt, and very effective when you just want to *find the thing they tried to hide*.

---

## 🔄 What Are Threads?

The `-t` flag controls how many parallel requests Gobuster makes. More threads = faster brute-forcing, but also a higher risk of:
- Getting rate-limited
- Overwhelming the server

Not all modes need threading (e.g., simple DNS lookups), but for web-based fuzzing or file enumeration, it helps speed things up significantly.

Default: 10 threads

---

## 🧭 Mode: `dir` (Directory Brute-forcing)

### 🧰 Use Case:
You're testing a website like `http://insecure-portal.com` and you suspect there are admin pages, dev folders, or hidden files that aren't linked anywhere public.

### 🔧 Syntax:
```bash
gobuster dir -u http://insecure-portal.com -w /usr/share/wordlists/dirb/common.txt
```

### 🔑 Important Flags:
| Flag         | Purpose                                    |
| ------------ | ------------------------------------------ |
| `-u`         | Target URL                                 |
| `-w`         | Wordlist path                              |
| `-x`         | Append file extensions (e.g. `.php,.html`) |
| `-s`         | Show only specific status codes            |
| `--wildcard` | Detect custom 404 behavior                 |
| `-t`         | Threads to use                             |

### 📤 Sample Output:
```
===============================================================
Gobuster v3.6
===============================================================
[+] Url: http://insecure-portal.com
[+] Threads: 20
[+] Wordlist: /usr/share/wordlists/dirb/common.txt
===============================================================
Found: /index.php        (Status: 200)
Found: /hidden.html      (Status: 200)
Found: /backup           (Status: 403)
Found: /admin            (Status: 403)
```

### 🧪 With Extensions:
```bash
gobuster dir -u http://site.com -w common.txt -x php,html
```
Adds `.php` and `.html` to each word in the wordlist:
```
Trying: /login.php
Trying: /dashboard.html
```

### 🧪 With Status Code Filter:
```bash
gobuster dir -u http://site.com -w common.txt -s 200,403
```
Only show results with `200 OK` or `403 Forbidden`:
```
Found: /admin (Status: 403)
Found: /login.php (Status: 200)
```

### 🧪 With Wildcard Detection:
```bash
gobuster dir -u http://weirdsite.com -w small.txt --wildcard
```
Handles sites where **every wrong URL returns a fake 200**:
```
Wildcard response detected: all 404s show as 200
Filtering...
```

---

## 🌐 Mode: `dns` (Subdomain Discovery)

### 🧰 Use Case:
You're testing `example.com`, but you think there are hidden subdomains like `test.example.com`, `admin.example.com`, or `staging.example.com`.

### 🔧 Syntax:
```bash
gobuster dns -d example.com -w subdomains.txt -t 25
```

### 🔑 Important Flags:
| Flag | Purpose                  |
| ---- | ------------------------ |
| `-d` | Target domain            |
| `-w` | Wordlist with subdomains |
| `-t` | Threads (default: 10)    |

### 📤 Sample Output:
```
Found: dev.example.com
Found: admin.example.com
Found: legacy.example.com
```

---

## 🏠 Mode: `vhost` (Virtual Host Discovery)

### 🧰 Use Case:
You're targeting an IP or a domain, but you suspect **multiple web apps are hosted behind a shared IP** using virtual hosts.

### 🔧 Syntax:
```bash
gobuster vhost -u http://target-ip -w vhosts.txt -t 30
```

### 🔑 Important Flags:
| Flag | Purpose                          |
| ---- | -------------------------------- |
| `-u` | Base domain or IP to test        |
| `-w` | Wordlist with virtual host names |
| `-t` | Threads                          |

### 📤 Sample Output:
```
Found: dev.site.com
Found: staging.site.com
Found: test.site.com
```

---

## 🎯 Mode: `fuzz` (Custom Fuzzing)

### 🧰 Use Case:
You want to fuzz a specific part of a URL or parameter. For example, you're not brute-forcing whole directories, just **a single point** in a URL.

### 🔧 Syntax:
```bash
gobuster fuzz -u https://target.com/api/FUZZ -w endpoints.txt -t 15
```

### 🔑 Important Flags:
| Flag | Purpose                                |
| ---- | -------------------------------------- |
| `-u` | URL with FUZZ keyword                  |
| `-w` | Wordlist of values to insert into FUZZ |
| `-t` | Threads                                |

### 📤 Sample Output:
```
/api/login            (Status: 200)
/api/debug            (Status: 403)
/api/panel            (Status: 401)
```

---

## ✅ Quick Mode Reference

| Mode    | When To Use                                                           |
| ------- | --------------------------------------------------------------------- |
| `dir`   | Finding hidden folders/files on a site (e.g. `/admin`, `/backup.zip`) |
| `dns`   | Discovering subdomains (e.g. `test.example.com`)                      |
| `vhost` | Finding virtual hosts on shared servers/IPs                           |
| `fuzz`  | Targeted fuzzing of URL segments or parameters                        |

---

## 🧠 Pro Tips
- Use `--wildcard` if everything returns 200 — custom 404s are tricking you.
- 403 is a win. It means something is there.
- If all you get is 404, maybe you're on the wrong path or rate-limited.
- Use a wordlist appropriate to the target (start small, escalate).
- Use `-t` to adjust speed vs stealth: fewer threads = stealthier scans.

---

## 🔗 References
- [Gobuster GitHub](https://github.com/OJ/gobuster)
- [SecLists](https://github.com/danielmiessler/SecLists)

