
# Home Lab SOC — Capture Analysis

## Capture 1 (no GET)
- File: captures/first-capture.pcapng
- Screenshot: analysis/first-capture-screenshot.jpg
- Notes: Captured HTTP traffic headers (Host and User-Agent). GET request not explicitly shown.


## Capture 2 (GET)
- File: captures/http-get-capture.pcapng
- Screenshot: analysis/http-get-screenshot.jpg
- Notes: Captured HTTP GET request to neverssl.com. Request method GET is visible along with Host and User-Agent. Demonstrates successful HTTP request capture.


  ## Capture 3 — DNS Query
- File: captures/dns-capture.pcapng
- Screenshot:
- analysis/dns-screenshot-1.jpg
- analysis/dns-screenshot-2.jpg
- Notes:
  - Captured DNS query for a custom subdomain (e.g., `test-log.savage.neverssl.com`).
  - Packet details show Query Name, Query Type, and DNS server response.
  - Demonstrates ability to identify DNS traffic, inspect DNS questions/answers, and correlate network behavior.


## Capture 4 — Local Port Scan (127.0.0.1 ports 2000–2010)
- File: captures/scan-capture.pcapng
- Screenshots: 
  - analysis/scan-screenshot-1.jpg  
  - analysis/scan-screenshot-2.png  
- Notes:
  - Simulated port scan using `nc` (netcat) to send SYN packets to ports 2000–2010.
  - Wireshark captured repeated SYN attempts and corresponding RST responses (common behavior for closed ports).
  - Demonstrates understanding of TCP flags, reconnaissance patterns, and packet filtering techniques.
  - This type of pattern would trigger alerts in a real SOC for potential reconnaissance activity.
