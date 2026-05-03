# WhoDisIP | BS Reviews Intelligence

> [!TIP]
> ### 🛠️ Support & Issues
> This is a 100% free, open-source tool. We do not sell "premium support" or corporate services.
>
> * **🐛 Bug Reports:** Found a glitch or a broken API? Please open a public [Issue on GitHub](https://github.com/dextyix/WhoDisIP/issues).

**Maintained by [BS Reviews](https://bsreviews.com)**

---

## Overview

**WhoDisIP** is a lightweight, zero-BS, browser-based OSINT tool designed for rapid infrastructure mapping. We built this to quickly resolve domains, identify shady hosting providers, and pull geolocation data without relying on bloated, server-side tracking infrastructure.

**What it actually does:**
- **Dual-Stack Resolution:** Automatically detects and resolves both IPv4 and IPv6.
- **Infrastructure Mapping:** Exposes the true ISP, Hosting Provider, and Organization behind an IP.
- **Registrar Data:** Pulls Domain Registrar info directly via RDAP.
- **DNS Recon:** Grabs active authoritative Nameservers.
- **Geolocation:** Pinpoints City, Country, and Timezone.

---

## Stable Release

✅ **v1.0.0 Stable** - This tool is production-ready.
If you hit a weird edge case or find a domain that breaks the scanner, drop an issue on GitHub so we can patch it.

---

## Requirements

- **Modern Web Browser** (Chrome, Firefox, Brave, Edge).
- **Internet Connection** (It needs to hit public APIs to fetch data).
- *Optional:* Drop it on literally any static web server (Apache, Nginx, or GitHub Pages) for live hosting.

---

## Installation

WhoDisIP is a **Single File Application**. No PHP, no Node.js, no databases, no server-side bloat.

1. Clone or download this repository.
2. Upload the HTML file to your web server (or just double-click it to open locally in your browser).
3. That's it. It works immediately.

---

## Usage

1. Throw a **Target** into the input field.
   - Accepts **IPv4** (e.g., `8.8.8.8`)
   - Accepts **IPv6** (e.g., `2001:4860:4860::8888`)
   - Accepts **Domains** (e.g., `bsreviews.com`)
2. Click **Analyze**.
3. Instantly get the data:
   - Resolved IP Address
   - Nameservers (if it's a domain)
   - True Hosting Provider / ISP
   - Domain Registrar
   - Physical Location & Timezone

---

## ⚠️ Architecture & Limits (Read This)

WhoDisIP operates entirely **Client-Side**. That means all API requests are fired directly from the **user's browser**, not your web server.

### 🚀 Why Client-Side?
Because it protects your infrastructure.
- **No Server IP Bans:** You can host this tool for 10,000 concurrent users without your server's IP address getting blacklisted by the APIs.
- **Distributed Rate Limits:** API usage limits apply to the *visitor's* IP address. If some idiot decides to spam the analyze button, they only rate-limit themselves. Everyone else stays online.

### 🛑 The API Limits (Per Visitor)
We rely on free-tier public endpoints. They enforce limits per user:
- **Geolocation (`ipapi.co` & `GeoJS`):** We use a dual-provider failover system. If a user hits a rate limit on the primary provider, the free unlimited fallback instantly takes over.
- **Registrar Data (`rdap.org`):** ~10 requests per 10 seconds.
- **DNS Resolution (`dns.google`):** Massive capacity, extremely unlikely to be rate-limited.

*If a user hits a wall, they get an error until their cooldown period expires.*

### 🔒 Privacy Blockers & GDPR
- **Adblockers:** Aggressive privacy extensions (like strict uBlock Origin settings or Brave Shields) might block the cross-origin (CORS) requests needed to fetch the data. If the tool fails, check the extensions.
- **Registrar Privacy (GDPR):** A lot of domain registries heavily redact ownership data now. In these cases, the tool will explicitly state "Registry Restricted / Redacted".

---

## APIs & Data Sources

No hidden backend tracking. The browser queries these public APIs directly:

- **Google DNS (DoH)** - For pure A/AAAA/NS record resolution (safely ignoring CNAME wrappers).
- **RDAP.org** - For Domain Registrar identification.
- **ipapi.co & GeoJS** - A robust dual-failover system for Geolocation and ISP mapping.

---

## License

This project is licensed under the **[GPLv3 License](https://www.gnu.org/licenses/gpl-3.0.html)**.  
You may use, modify, and redistribute the module **as long as credit is preserved** and your derivatives remain open source.

---

## Credits

- **[BS Reviews](https://bsreviews.com)** – Project Maintainers
- **[Dex (@dextyix)](https://github.com/dextyix)** – Founder & Lead Developer