# Burp Suite Community Edition: Setup and First Use Guide

> Your guide to installing, configuring, and surviving your first Burp-powered browser interception session.

---

## ☕ 1. Java Check & Install (If Needed)

### 🔍 Check if Java is Installed

```bash
java -version
```

If Java is not recognized, install it:

- Go to [https://www.java.com/en/download/manual.jsp](https://www.java.com/en/download/manual.jsp)
- Download the **64-bit Windows Offline** installer
- Run and install Java Runtime Environment (JRE)

---

## 📦 2. Install Burp Suite Community Edition

- Download from: [https://portswigger.net/burp/communitydownload](https://portswigger.net/burp/communitydownload)
- Run the installer
- Install to default directory
- Launch Burp from Start Menu or desktop

---

## 🌐 3. Configure Proxy in Firefox

### Option A: Manual Proxy Setup

- Open Firefox → `about:preferences`
- Scroll to bottom → **Network Settings** → **Settings...**
- Select: `Manual proxy configuration`
- Set:

```
HTTP Proxy: 127.0.0.1
Port: 8080
[x] Use this proxy server for all protocols
[ ] Uncheck all other options
```

- Click OK

### Option B: Use FoxyProxy

- Install from: [FoxyProxy on Mozilla Add-ons](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/)
- Create a new proxy profile:

```
Name: Burp
Proxy IP: 127.0.0.1
Port: 8080
[x] Use for all protocols
```

- Activate it via the toolbar fox icon

---

## 🔐 4. Install Burp's CA Certificate in Firefox

- Make sure Firefox is using the proxy (above)
- Visit `http://burp` in Firefox (Burp must be running)
- Download `cacert.der`
- Go to Firefox → `Settings` → `Privacy & Security`
- Scroll to **Certificates** → **View Certificates**
- Go to **Authorities** → **Import...**
- Select `cacert.der` → check:
  - ☑️ Trust this CA to identify websites

---

## 🧪 5. Test Your Setup

- In Firefox, visit: `http://example.com` or `http://httpbin.org/ip`
- In Burp → **Proxy > HTTP History**: You should see the request
- If it doesn't work:
  - Clear Firefox cache
  - Restart Firefox and Burp
  - Re-check proxy settings

---

## 🧰 Bonus Tools

### Built-in Chromium Browser

- Use Burp's built-in browser (Proxy > Intercept > Open Browser)
- Already configured to work with Burp

### Repeater

- Send any request to Repeater (Right click > Send to Repeater)
- Modify and resend requests freely

---

## 🎯 Suggested Next Steps

### TryHackMe: **Burp Suite: The Basics**

- Beginner-friendly
- Hands-on guided exercises
- Covers intercepting, Repeater, Intruder basics
- [https://tryhackme.com/room/burpsuitebasics](https://tryhackme.com/room/burpsuitebasics)

### PortSwigger Web Security Academy

- Free, in-browser labs
- Official Burp tutorials with labs for Repeater, Proxy, and more
- [https://portswigger.net/web-security](https://portswigger.net/web-security)

### Custom Mini Exercises

1. Visit `http://httpbin.org/get` and replay with different headers
2. Intercept a login form, replay it in Repeater
3. Spoof User-Agent and X-Forwarded-For headers
4. Try changing GET to POST and observe responses
5. Use OPTIONS method and review supported verbs

---

## 📚 Resources

- [Burp Suite Docs](https://portswigger.net/burp/documentation)
- [FoxyProxy Setup Tutorial](https://foxyproxy.com/support.html)
- [MDN Proxy Configuration Docs](https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Configuring_Firefox_to_use_a_proxy_server)

---

