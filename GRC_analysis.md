# GRC Analysis — Unauthorized Web Access Attempt

**Exercise:** Detecting and Documenting Unauthorized Web Access Attempts
**Author:** Gene Crittenden
**Date:** 2025-11-13
**Environment:** Isolated VirtualBox host-only network lab

---

## 1. Governance

- **Purpose:** Establish clear documentation and procedures for handling web server access attempts.
- **Policy Considerations:**
- Maintain comprehensive logging of all web server activity.
- Periodically review logs for unauthorized access attempts.
- Ensure lab exercises are performed in a controlled environment to avoid operational risk.

- **Roles & Responsibilities:**
- **SOC Analyst:** Monitors and analyzes web server logs, identifies suspicious behavior.
- **Compliance Officer / Auditor:** Ensures exercise aligns with organizational GRC frameworks and policies.

---

## 2. Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| Unauthorized web access / reconnaissance | Medium (lab-simulated) | Low (lab environment) | Implement controlled lab networks, isolate virtual machines |
| Exposure of sensitive logs | Low | Medium | Sanitize logs before sharing; store locally if containing real IPs |
| Misconfigured web server | Low | Medium | Use default secure nginx configuration; test in isolated environment |

---

## 3. Compliance & Control Mapping

| Framework | Control / Requirement | Relevance to Exercise |
|-----------|--------------------|---------------------|
| **NIST SP 800-53** | SI-4: Information System Monitoring | Monitoring and logging web access for detection of suspicious activity |
| **ISO 27001:2022** | A.8.16 Monitoring Activities | Periodic log review and monitoring for security events |
| **CIS Controls v8** | 13.1: Centralized Security Event Alerting | Demonstrates capturing and analyzing web server logs for unusual requests |

---

## 4. Recommendations

- Maintain **log retention and review policy** for both production and lab environments.
- Implement **segregation of duties** for monitoring, analysis, and compliance documentation.
- Perform **periodic GRC reviews** to ensure lab exercises simulate real-world risk scenarios safely.
- Document all exercises clearly, including logs, screenshots, and analysis, to create **audit-ready records**.

---

## 5. Lessons Learned

- Even controlled lab exercises can demonstrate GRC best practices when logs, policies, and risk assessment are included.
- Mapping incidents to multiple frameworks (NIST, ISO, CIS) helps illustrate **compliance relevance**.
- Documenting findings in a structured format prepares students and practitioners for real-world audit and compliance workflows.

---

## 6. Supporting Files

- Logs: `logs/access_sanitized.txt` `logs/error_sanitized.txt`
- Incident report: `incident_report.md`
- Screenshots: `screenshots/nginx_log_view.png`, `screenshots/curl_requests.png`
- README: `README.md`
