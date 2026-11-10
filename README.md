# Penetration Testing Report: Footprinting & Network Scanning (Week 2)

## 📌 Project Overview
This project documents the execution of reconnaissance, passive footprinting, and active local network scanning as part of the Networkwalks Cybersecurity Internship (Week 2)[cite: 38]. 

- **Target Scope:** `networkwalks.com` (Non-destructive footprinting with written authorization) & Local LAN Subnet (Self-owned environment)[cite: 38, 40].
- **Modules Covered:**
  - **W2-PM1:** Footprinting & Reconnaissance Attacks with Multiple Kali Tools[cite: 38, 43, 99]
  - **W2-PM5:** Network Scanning and Topology Discovery with Zenmap[cite: 38, 88, 99]

---

## 🛠️ Tools Used & Objectives
| Tool | Platform | Operational Purpose |
| :--- | :--- | :--- |
| **WHOIS** | Kali Linux | Domain registration, creation/expiry timelines, and authoritative nameservers[cite: 38, 44] |
| **WhatWeb** | Kali Linux | Fingerprinting web server engines, CMS frameworks, and active plugins[cite: 38, 45] |
| **nslookup** | Kali Linux | DNS host-to-IP resolution[cite: 38, 46] |
| **curl -I** | Kali Linux | HTTP/HTTPS header extraction, banner grabbing, and API endpoints[cite: 38, 47] |
| **wafw00f** | Kali Linux | Web Application Firewall (WAF) detection and fingerprinting[cite: 38, 48] |
| **dnsrecon** | Kali Linux | Enumeration of DNS resource records (NS, MX, SPF, TXT, SRV)[cite: 38, 49] |
| **Zenmap (Nmap GUI)**| Windows | Local subnet ping sweeps, live host identification, and topology mapping[cite: 38, 88] |

---

## 🔍 Module Execution & Findings

### 1. W2-PM1: Footprinting (networkwalks.com)
- **WHOIS:** Registrar identified as GoDaddy.com, LLC; domain name servers delegated to HostGator (`NS6135.HOSTGATOR.COM`, `NS6136.HOSTGATOR.COM`)[cite: 44].
- **WhatWeb:** Target detected running an Apache web server, WordPress CMS, and WordPress Download Manager plugin (`wpdm_client` session tracking)[cite: 45].
- **nslookup:** Resolved the apex domain `networkwalks.com` to IPv4 address `192.232.216.135`[cite: 46].
- **curl -I:** Returned HTTP/2 200 OK status, exposing Apache server banners, endurance cache levels, and WordPress REST API routes (`/wp-json/`)[cite: 47].
- **wafw00f:** Fingerprinted an active **ModSecurity (SpiderLabs)** Web Application Firewall protecting the web application[cite: 48].
- **dnsrecon:** Enumerated mail exchangers (`mail.networkwalks.com`), SPF authentication records (`v=spf1`), BIND version disclosure, and cPanel autodiscover SRV records[cite: 49].

### 2. W2-PM5: Local Network Scanning (Zenmap)
- **Target Subnet:** `10.223.163.0/24`[cite: 88, 92]
- **Scan Type:** Nmap Ping Scan (`nmap -sn 10.223.163.0/24`)[cite: 87, 92]
- **Host Discovery:** Successfully mapped live IP and MAC addresses across the active Wi-Fi subnet[cite: 87, 93].
- **Network Topology:** Rendered and exported graphic topology to PDF (`Zenmap-Topology.pdf`)[cite: 94].

---

## 📸 Lab Evidence & Screenshots

### Module W2-PM1 Evidence (Kali Linux)
#### 1. WHOIS Lookup
<img width="958" height="299" alt="Screenshot 2026-11-10 194632" src="https://github.com/user-attachments/assets/64212148-f7b2-4add-beae-923b101e7cd3" />


#### 2. WhatWeb Fingerprint
<img width="956" height="233" alt="Screenshot 2026-11-10 194829" src="https://github.com/user-attachments/assets/3384681f-bd22-41ff-8c88-8f3c2a8f9ca3" />

#### 3. Nslookup DNS Resolution
<img width="951" height="161" alt="Screenshot 2026-11-10 194904" src="https://github.com/user-attachments/assets/b7f7e14a-18cd-478e-b842-bb9dc5811982" />


#### 4. HTTP Headers via cURL
<img width="959" height="206" alt="Screenshot 2026-11-10 195002" src="https://github.com/user-attachments/assets/b42c1266-e74b-43e9-968b-927604611426" />


#### 5. WAF Detection via Wafw00f
<img width="953" height="299" alt="Screenshot 2026-11-10 195057" src="https://github.com/user-attachments/assets/ff05dfd9-e683-4047-b6ca-d4f5c415aa94" />


#### 6. DNS Record Enumeration via DNSRecon
<img width="951" height="306" alt="Screenshot 2026-11-10 195203" src="https://github.com/user-attachments/assets/9bc05d48-4384-4909-b7ae-e53af1be5182" />


---

### Module W2-PM5 Evidence (Zenmap)
#### 7. Zenmap Nmap Ping Scan Output
<img width="959" height="503" alt="Screenshot 2026-11-10 201312" src="https://github.com/user-attachments/assets/1d778827-c16f-4e78-8a42-c1994a50514d" />


#### 8. Network Topology Map & Legend
<img width="959" height="505" alt="Screenshot 2026-11-10 202310" src="https://github.com/user-attachments/assets/56c500fb-856d-4e12-8675-30138c88b5f1" />

---

## 🔧 Troubleshooting Experience
- **Issue:** During Module W2-PM5, attempting to save the network topology PDF triggered the error `Error saving snapshot: error while writing to output stream`
- **Root Cause:** Zenmap defaulted to saving inside `C:\Program Files (x86)\Nmap\`, which has write-protection restrictions for standard processes under Windows
- **Resolution:** Redirected the output destination to the local user directory (`Desktop`), successfully exporting `Zenmap-Topology.pdf`

---

## ⚖️ Liability & Scope Disclaimer
All testing activities were performed strictly under authorization (Reference: Networkwalks Letter of Authorization NW-LOA-B082-017) and within the self-owned local lab environment for educational purposes
