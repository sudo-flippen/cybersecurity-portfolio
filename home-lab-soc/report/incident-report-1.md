# Incident Report — Home Lab SOC Simulation

**Incident ID:** HLS-001  
**Date:** 2025-12-08  
**Reported by:** Logan Flippen  

---

## 1. Executive Summary
This simulated home-lab exercise demonstrates the ability to capture, analyze, and document network events using Wireshark. The project includes four captures:

1. HTTP traffic (headers only)
2. Full HTTP GET request
3. DNS query for a unique subdomain
4. Local port scan (reconnaissance simulation)

These captures reflect common patterns SOC Analysts monitor during routine investigations, such as DNS anomalies, HTTP requests, and reconnaissance behaviors like SYN-only scans.


## 2. Timeline of Events
**Capture 1 — HTTP Headers Only**  
- Event: Curl request generated simple HTTP traffic  
- Notes: GET not visible; captured Host & User-Agent headers  

**Capture 2 — HTTP GET Request**  
- Event: HTTP GET to `neverssl.com`  
- Notes: GET method, Host, and User-Agent successfully captured  

**Capture 3 — DNS Query**  
- Timestamp: **4.763403**  
- Query Name: `test-log.Savage.neverssl.com`  
- Source IP: **192.168.108.151**  
- Destination (DNS server): **192.168.108.1**  
- Notes: DNS query captured; included question section and server response  

**Capture 4 — Local Port Scan**  
- Time Range: **17.169277 → 17.270611**  
- Packet Numbers: **Packets #127–#147**  
- Behavior: Sequential SYN packets to ports 2000–2010  
- Interpretation: Repeated SYNs with no ACKs = reconnaissance behavior  


## 3. Technical Analysis

### HTTP Traffic  
- Demonstrated ability to filter, decode, and inspect HTTP packets.  
- Identified request methods, Host headers, and browser/user-agent info.

### DNS Query  
- Observed DNS question for custom subdomain (`test-log.Savage.neverssl.com`)  
- Validated DNS resolution path and inspected Question/Answer sections  
- Demonstrated skill in identifying DNS patterns relevant to phishing or C2 traffic

### Local Port Scan (Simulated Using `nc`)  
- Sequential SYN packets resemble malicious scanning behavior  
- Destination ports 2000–2010 were closed, resulting in RST responses  
- Mirrors behaviors seen during threat reconnaissance  
- Shows ability to use network tools to generate test data for investigation

**Explanation of simulated scan:**  
Netcat (`nc`) was used to safely attempt connections to localhost ports 2000–2010.  
Each attempt sends a SYN packet; closed ports return RST.  
This pattern is commonly flagged by SIEMs as port scanning or probing activity.


## 4. Indicators of Compromise (IoCs)

**DNS IoC**
- Query: `test-log.Savage.neverssl.com`  
- Source IP: 192.168.108.151  
- Destination (DNS server): 192.168.108.1  
- Timestamp: 4.763403  

**Network Scan IoC**
- Localhost scan: 127.0.0.1 ports **2000–2010**  
- Packet Range: **#127–#147**  
- Time Range: **17.169277 → 17.270611**  
- Behavior: Repeated SYN packets without ACKs (reconnaissance pattern)


## 5. Impact Assessment
This exercise took place entirely inside a controlled home machine environment.  
There was **no risk** to external systems.  
However, these packet patterns reflect real-world events SOC teams investigate regularly.


## 6. Recommendations
1. Create SIEM rules to alert on:  
   - Excessive SYN traffic  
   - Sequential port patterns  
   - Unusual DNS queries  
2. Correlate DNS traffic with known malicious domains  
3. Capture host logs to identify processes generating scans  
4. Expand lab by adding Splunk or Wazuh to demonstrate automated detection


**Report Prepared By:**  
**Logan Flippen**  
Home Lab SOC Project
