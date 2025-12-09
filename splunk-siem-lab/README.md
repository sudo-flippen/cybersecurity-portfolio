# Splunk SIEM Detection Lab

This project simulates a real-world SOC (Security Operations Center) workflow using Splunk Cloud.  
Multiple log sources were ingested, analyzed, and correlated to detect brute-force attacks, port scans, and web exploitation attempts.

This lab demonstrates my ability to:
- Ingest multi-source security logs into a SIEM  
- Run SPL detection queries  
- Extract indicators of compromise (IoCs)  
- Identify attacker behavior  
- Document findings in a professional incident report  

---

## 🎯 Project Objective

Build a mini SIEM environment using Splunk Cloud and detect the following:

1. **Authentication attacks** (brute-force attempts)  
2. **Web exploitation attempts** (XSS, SQL patterns, suspicious POST requests)  
3. **Port scanning behavior** (multi-port reconnaissance)  
4. **Cross-log correlation** to form a complete attack timeline  

This project mirrors the work of a Tier-1 SOC Analyst.

---

## 🧰 Tools & Technologies

- **Splunk Cloud (Free Trial)**  
- **SPL (Search Processing Language)**  
- **Log Sources:**  
  - Authentication logs (`auth.log`)  
  - Brute-force attack logs (`bruteforce.log`)  
  - Web access logs (`web.log`)  
  - Firewall logs (`firewall.log`)  
- **Regex field extraction** using `rex`  
- **GitHub** for documentation  

---

## 🔎 Detection Techniques Used

### ✔ Authentication Attack Detection
- Failed login enumeration  
- Brute-force pattern identification  
- Source IP extraction with regex  
- Successful login correlation  

### ✔ Web Attack Detection
- XSS payload identification (`<script>`)  
- SQL injection pattern detection  
- Suspicious POST upload behavior  

### ✔ Reconnaissance Detection
- Port scan analysis via firewall logs  
- Multi-port SYN/DROP correlation  
- High-value port targeting  

### ✔ Field Extraction with Regex
Used extensively due to `misc_text` sourcetype:
```spl
| rex "(?<src_ip>\d+\.\d+\.\d+\.\d+)"
| rex "DPT=(?<dest_port>\d+)"
