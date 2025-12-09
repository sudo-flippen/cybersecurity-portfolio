Splunk SIEM Incident Report — Home Lab Simulation

Incident ID: SIEM-001
Date: 2025-12-08
Prepared by: Logan Flippen



1. Executive Summary

This report documents a simulated security incident recreated in a home SOC environment using Splunk Cloud. Multiple log sources were analyzed, including authentication logs, firewall logs, brute-force logs, and web server access logs.

Across the four data sources, coordinated attacker behavior was observed:
	•	Systematic brute-force attempts
	•	Web exploitation attempts (XSS)
	•	A focused unauthorized file upload request
	•	Multi-port reconnaissance (port scan)

These events collectively represent a full kill-chain sequence often seen in real-world attacks.



2. Timeline of Events

12:01:15–12:01:18

Brute-force cluster from 185.123.44.21 (3 failed logins)

12:01:28

Failed login from 92.14.55.2

12:02:04

Successful login from host IP 192.168.108.151

12:02:15

Failed login from 77.23.66.8

12:03:11

Failed login from 185.123.44.21

12:11:01–12:12:45

Web attacks begin:
	•	SQL/XSS pattern from 92.14.55.2
	•	Suspicious POST upload (HTTP 500) from 77.23.66.8

12:20:11–12:20:25

Brute-force log shows 5 rapid authentication failures from 185.123.44.21

Throughout window

Firewall records show port scanning from 185.123.44.21 targeting:
22, 80, 443, 3306, 8080



3. Technical Analysis

A. Authentication Activity
	•	Total Failed Password Attempts: 7
	•	Primary attacker: 185.123.44.21
	•	Indicates brute-force spraying behavior
	•	Successful login occurred between failed attempts (common attacker tactic)

B. Brute-Force Log
	•	5 rapid attempts in 14 seconds
	•	From 185.123.44.21
	•	Behavior matches automated attack tooling (e.g., Hydra, Medusa)

C. Web Exploitation Attempts
	•	<script>alert('XSS') request from 92.14.55.2
	•	Attempted SQL-style login bypass from earlier logs
	•	Suspicious POST upload attempt from 77.23.66.8
	•	HTTP 500 indicates backend processing failure
	•	Could represent malicious file upload attempt

D. Firewall Reconnaissance

Attacker 185.123.44.21 scanned multiple high-value ports:

22,
SSH,
Password attack or key-based intrusion


80,
HTTP,
Discovery of web services


443,
HTTPS,
Enumeration of TLS endpoints


3306,
MySQL,
Database exploitation attempts


8080,
Web/admin consoles,
Vulnerable admin interfaces



4. Indicators of Compromise (IoCs)

IP Addresses
	•	185.123.44.21 – Port scanning + brute force
	•	92.14.55.2 – XSS attack
	•	77.23.66.8 – Suspicious POST upload
	•	192.168.108.151 – Legitimate login

URLs / Payloads
	•	<script>alert('XSS')</script>
	•	login.php?user=admin' OR '1'='1
	•	/api/upload (500 error)



5. Impact Assessment
	•	No systems were harmed — all activity occurred in a controlled lab environment.
	•	The simulated attack chain reflects real-world intrusion phases, including:
	•	Reconnaissance
	•	Credential attacks
	•	Web exploitation
	•	Suspicious file interaction

This environment successfully demonstrates capability in log aggregation, pattern detection, and threat analysis.



6. Recommendations
	1.	Implement account lockout policies for repeated failures
	2.	Enable MFA to prevent credential-based compromise
	3.	Add WAF rules to block XSS injection attempts
	4.	Restrict SSH access to known trusted IPs
	5.	Monitor file uploads for anomalous requests
	6.	Deploy SIEM alert rules for:
	•	Excessive login failures
	•	XSS payloads
	•	SQL injection patterns
	•	Port scans (SYN fan-out behavior)



7. Conclusion

This simulated incident demonstrates the ability to:
	•	Ingest multi-source logs
	•	Analyze diverse attack patterns
	•	Identify IoCs
	•	Build a coherent incident timeline
	•	Document findings professionally

