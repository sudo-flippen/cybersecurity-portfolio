# Home Lab SOC Project — Network Capture, Analysis & Incident Reporting

This project simulates real Security Operations Center (SOC) workflows by generating safe network traffic, capturing it with Wireshark, analyzing packet behavior, identifying potential indicators of compromise (IoCs), and producing a professional incident report.  
It demonstrates critical skills used by entry-level SOC Analysts and Cybersecurity Analysts.



## Objectives
- Build a lightweight home SOC environment  
- Capture HTTP, DNS, and port scan traffic  
- Use Wireshark to analyze packet behavior  
- Identify suspicious or notable activity  
- Document findings using SOC-style reporting  
- Demonstrate technical communication and investigative skills  

## Tools Used
- **Wireshark** — Packet capture & protocol analysis  
- **macOS Terminal**  
  - `curl` (HTTP testing)  
  - `dig` (DNS queries)  
  - `nc` (netcat port scanning)  
- **GitHub** — Hosting documentation & artifacts  



## Captures Included

### **Capture 1 — HTTP Traffic (Headers Only)**
- Basic HTTP request generated with `curl -I`  
- Captured Host and User-Agent headers  

### **Capture 2 — Full HTTP GET Request**
- Full GET request captured using `curl -v`  
- Shows method, host, and user-agent fields  

### **Capture 3 — DNS Query**
- Custom DNS lookup: `test-log.<username>.neverssl.com`  
- Shows Question/Answer sections  
- Demonstrates DNS investigation skills  

### **Capture 4 — Local Port Scan**
- Reconnaissance-style SYN scan using `nc`  
- Sequential SYN packets to ports 2000–2010  
- Demonstrates ability to identify scan behavior  



## Folder Structure

home-lab-soc/
├── analysis/
│   ├── analysis.md
│   ├── dns-screenshot-1.jpg
│   ├── dns-screenshot-2.jpg
│   ├── first-capture-screenshot.jpg
│   ├── http-get-screenshot.jpg
│   ├── scan-screenshot-1.jpg
│   └── scan-screenshot-2.jpg
│
├── captures/
│   ├── dns-capture.pcapng
│   ├── first-capture.pcapng
│   ├── http-get-capture.pcapng
│   └── scan-capture.pcapng
│
└── report/
└── incident-report-1.md
├── README.md



## Key Skills Demonstrated
- Packet capture & network analysis  
- HTTP, DNS, and TCP protocol inspection  
- Detection of reconnaissance behavior (SYN scan)  
- Use of Wireshark filters  
- Identifying Indicators of Compromise (IoCs)  
- Technical documentation & incident reporting  
- GitHub project organization  
- Reproducible SOC workflow  



## How to Reproduce This Project

**### **1. Generate HTTP Traffic**
curl -I http://neverssl.com
curl -v http://neverssl.com

### **2. Generate DNS Query**
dig +short test-log.$(whoami).neverssl.com

### **3. Generate a Local Port Scan**
for p in {2000..2010}; do nc -zv 127.0.0.1 $p 2>&1 | head -n 1; done

### **4. Analyze packets in Wireshark**
Recommended filters:
http
dns
tcp && ip.addr == 127.0.0.1
tcp.flags.syn == 1



Created by:
Logan Flippen
