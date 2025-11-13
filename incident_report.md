# Incident Report —  Unauthorized Web Access Attempt

**Incident ID:** SOC-001
**Date/Time:** 2025-11-13
**Reported By:** Gene Crittenden
**Environment:** Isolated VirtualBox host-only network lab
**Systems Involved:** `web-server` VM running nginx, `client` VM using curl

---

## 1. Summary

Multiple unauthorized HTTP access attempts were detected targeting the nginx web server.
The activity was generated in a controlled lab environment to simulate common reconnaissance and scanning behaviors.

---

## 2. Details of the Event

| Field | Description |
|-------|-------------|
| **Source IP** | 192.168.56.102 (`client` VM) |
| **Destination IP** | 192.168.56.101 (`web-server` VM) |
| **Targeted URLs** | `/admin`, `/login.php`, `/../../etc/passwd` |
| **User-Agent Observed** | `curl/7.xx`, `sqlmap/1.0` |
| **HTTP Status Codes** | 404 (Not Found) for all suspicious attempts |
| **Log Evidence** | See `logs/access_sanitized.txt` for sample entries |

**Observation:**
The malicious requests included URL paths commonly used for enumeration or directory traversal. The requests did not succeed in accessing sensitive content (expected in the lab environment).

---

## 3. Analysis

- **Indicators of Compromise:**
- Requests for non-existent admin paths
- Suspicious user-agent strings (`sqlmap`)
- Repeated failed requests in a short timeframe

- **Impact:**
- None — isolated lab environment
- Logs captured all activity for analysis

- **Severity:** Low
- **Likelihood of recurrence:** High in real environments if a vulnerable server is exposed

---

## 4. SOC Recommendations

1. Ensure **centralized logging** and regular log review.
2. Monitor for **patterns of enumeration** and failed access attempts.
3. Implement automated **IP blocking or rate limiting** for repeated suspicious requests.
4. Maintain test logs in sanitized form for **training and documentation purposes**.

---

## 5. GRC Framework Mapping

| Framework | Control | Relevance |
|-----------|---------|-----------|
| **NIST SP 800-53** | SI-4: Information System Monitoring | Ensures monitoring of web server logs to detect suspicious activity |
| **ISO 27001:2022** | A.8.16: Monitoring Activities | Supports periodic review of web access and detection of unauthorized requests |
| **CIS Controls v8** | 13.1: Centralized Security Event Alerting | Highlights the importance of collecting and analyzing logs for potential threats |

---

## 6. Actions Taken

- Captured and reviewed logs from nginx (`access.log`, `error.log`)
- Sanitized logs for safe documentation (`access_sanitized.txt`)
- Created this incident report for SOC and GRC review

---

## 7. Lessons Learned

- Even small lab servers generate valuable forensic evidence.
- Consistent logging and log review are critical for early detection of probing attempts.
- Mapping incidents to GRC frameworks adds organizational context and compliance awareness.

---

## 8. References / Supporting Files

- Logs: `logs/access_sanitized.txt` `logs/error_sanitized.txt`
- Screenshots: `screenshots/nginx_log_view.png`, `screenshots/curl_requests.png`
- README: [README.md](./README.md)
