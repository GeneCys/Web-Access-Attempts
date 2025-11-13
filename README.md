# Exercise 1 — Detecting and Documenting Unauthorized Web Access Attempts

### Objective
This exercise simulates unauthorized HTTP access attempts within a controlled virtual network environment.
The goal is to:
- Generate both normal and suspicious web traffic.
- Capture and analyze nginx access logs for evidence of probing or attacks.
- Produce an incident report with SOC and GRC perspectives.

---

### Lab Setup

| Component | Description |
|------------|--------------|
| **VM1 (web-server)** | Ubuntu Linux running nginx |
| **VM2 (client)** | Ubuntu Linux using curl for requests |
| **Network Type** | Host-only network |
| **Tools Used** | nginx, curl, tail, grep, bash |

**Network Configuration:**
- `web-server`: `192.168.56.101`
- `client`:     `192.168.56.102`

---

### Steps Performed

1. Installed and configured **nginx** on the web server.
2. Created a simple web page (`index.html`) served by nginx.
3. Generated **normal traffic** using:
- curl http://192.168.56.101/
4. Generated **suspicious traffic** using:
- curl http://192.168.56.101/admin
- curl http://192.168.56.101/login.php
- curl http://192.168.56.101/../../etc/passwd
- curl -A "sqlmap/1.0" http://192.168.56.101/
5. Collected and reviewed nginx logs from:
- /var/log/nginx/access.log
- /var/log/niginx/error.log
6. Documented findings in an **incident report** and mapped them to security frameworks.
