# Splunk SIEM Lab — Analysis Document

This file documents the technical steps, SPL queries, and observations from the Splunk SIEM lab.  
The goal was to detect authentication attacks, web exploitation attempts, and reconnaissance activity across multiple log sources.



## 1. Authentication Log Analysis (auth.log)

### **Query: Failed Password Attempts**

index=main host=soclab "Failed password"


Field Extraction for Source IPs

Because misc_text does not auto-extract fields, a regex was used:

index=main host=soclab "Failed password"
| rex "(?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| sort -count


Findings
	•	185.123.44.21 made multiple authentication failures
	•	92.14.55.2 attempted one failed login
	•	77.23.66.8 attempted one failed login
	•	A successful login occurred between failed attempts
	•	Pattern resembles brute-force spraying behavior

Screenshot Placeholder:
screenshots/auth-failures.png


## 2. Brute Force Log Analysis (bruteforce.log)

Query: View All Brute-Force Attempts
index=main host=soclab "Failed password"

Findings
	•	Five rapid failures from 185.123.44.21
	•	Attempts occurred between 12:20:11 – 12:20:25
	•	Attack speed suggests automated tooling (Hydra/Medusa-style)

Screenshot Placeholder:
screenshots/bruteforce.png


## 3. Web Exploitation Attempts (web.log)

SQL Injection Detection
index=main host=soclab "union select"
XSS Detection
index=main host=soclab "<script>"
If encoded:
index=main host=soclab "%3Cscript%3E"

Findings
	•	XSS attack detected from 92.14.55.2
	•	Suspicious POST upload attempt from 77.23.66.8
	•	Activity aligns with web exploitation reconnaissance

Screenshot Placeholder:
screenshots/web-attacks.png


## 4. Firewall Reconnaissance Analysis (firewall.log)

Port Scan Detection
index=main host=soclab "DROP"
| rex "SRC=(?<src_ip>\S+)"
| rex "DPT=(?<dest_port>\d+)"
| stats count by src_ip dest_port
| sort -count

Findings

Attacker 185.123.44.21 attempted connections to:
	•	Port 22 (SSH)
	•	Port 80 (HTTP)
	•	Port 443 (HTTPS)
	•	Port 3306 (MySQL)
	•	Port 8080 (Admin/API)

This represents systematic multi-port scanning.

Screenshot Placeholder:
screenshots/firewall-scan.png



## 5. Correlation Across Log Sources

Observed Attack Chain
	1.	Port scan from 185.123.44.21
	2.	Brute-force attempts on SSH
	3.	Web exploitation attempts (XSS + POST upload)
	4.	Repeated login failures mixed with a successful login
	5.	Secondary brute-force attempts

The logs show a complete simulated intrusion sequence:
	•	Recon → Credential attacks → Web exploitation → Persistence attempt


  ##      6. Skills Demonstrated  
	•	SIEM search and filtering
	•	SPL query building
	•	Field extraction using rex
	•	Threat pattern identification
	•	Cross-log correlation
	•	Technical documentation
	•	Incident investigation workflow
