# Detecting and Documenting Unauthorized Web Access Attempts

SOC-style exercise demonstrating unauthorized Web Access Attempts.

- **Author:** Gene Crittenden
- **Date:** 16 November 2025
- **Network Configuration:**
    - Web Server VM: `192.168.56.101`
    - Client VM:     `192.168.56.102`


## Objective

This lab demonstrates using **curl** to probe a web server for potential vulnerabilities or exploits on a local Apache web server. All work is performed on a **host-only VitrualBox network** with two VMs.

The goal is to:
- Generate both normal and suspicious web traffic.
- Capture and analyze nginx access logs for evidence of probing or attacks.
- Produce an incident report with SOC and GRC perspectives.

---

## Lab Setup

| Component | Description |
|------------|--------------|
| **VM1 (web-server)** | Ubuntu Linux running nginx |
| **VM2 (client)** | Ubuntu Linux using curl for requests |
| **Network Type** | Host-only network |
| **Tools Used** | nginx, curl, tail, grep, |

---

## Steps Performed

1. Installed and configured **nginx** on the web server.
2. Created a simple web page (`index.html`) served by nginx.
3. Generated **normal traffic** using:
```bash
curl http://192.168.56.101/
```
4. Generated **suspicious traffic** using:
```bash
curl http://192.168.56.101/admin
curl http://192.168.56.101/login.php
curl http://192.168.56.101/../../etc/passwd
curl -A "sqlmap/1.0" http://192.168.56.101/
```
5. Collected and reviewed nginx logs from:
```bash
/var/log/nginx/access.log
/var/log/niginx/error.log
```
6. Documented findings in an **Incident Report** and mapped them to security frameworks.

---

## Key Findings
- Detected multiple unauthorized HTTP acccess attempts (404 responses)
- Requests contained:
    - Suspicious paths (`/admin, /../../etc/passwd`)
    - Suspicious user-agent (`sqlmap/1.0`)
- All activity originated from the Client VM IP `293.268.56.102`

---

## SOC Analysis Summary
- Incident ID:   SOC-001
- Severity:      Low
- Impact:        None (controlled lab)
- Indicators:    Suspicious URL patterns, scanning user-agent
- Action Taken:  Logged event, recommended IP block, and log review procedure
Full details: incident_report.md

---

## GRC Framework Mapping
| Framework | Control | Description
|--------------|------------|-----------|
| NIST SP 800-53 | SI-4 | Information System Monitoring |
| ISO 27001:2022 | A.8.16 | Monitoring Activities |
| CIS Controls v8 | 13.1 | Centralize security event alerting and analysis |

---

## Skills Demonstrated

- Nmap NSE scripting & vulnerability scanning  
- Network traffic analysis with Wireshark  
- Vulnerability identification and remediation  
- Apache/Nginx configuration & hardening  
- SOC-style workflow: Detect → Remediate → Verify  
- Troubleshooting (port conflicts, configuration errors)

---

## Lessons Learned

- Even simple web servers reveal valuable forensic artifacts.
- Log monitoring is critical for early detection of probing or enumeration attempts.
- Linking SOC findins to GRC frameworks help build organizational context.

---

## Supporting Files
**Reports**
- [Incident Report](./incident_report.md)
- [GRC Report](./GRC_report.md)

[Logs](./logs)
- Nmap Scans & Wrieshark Packet Captures
  - _The original .pcapng file is kept offline and available upon request._

[Screenshots](./screenshots)
- Nmap Scans & Wireshark Filters

---

**End of Report**
