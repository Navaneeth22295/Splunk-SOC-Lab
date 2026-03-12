# Incident Investigation Report

---

## Incident Summary

| Field | Details |
|---|---|
| **Incident ID** | INC-2026-001 |
| **Date** | March 10, 2026 |
| **Analyst** | Navaneeth Sivaprasad |
| **Severity** | Critical / High / Medium / Low |
| **Status** | Open / Escalated / Closed |

---

## Alert Details

| Field | Details |
|---|---|
| **Alert Name** | e.g. Brute Force Detected |
| **Source** | Splunk SIEM |
| **Log Source** | WinEventLog / linux_secure |
| **Affected Host** | e.g. WORKSTATION-01 |
| **Affected User** | e.g. jsmith |
| **Source IP** | e.g. 185.220.101.34 |

---

## Timeline

| Time | Event |
|---|---|
| 08:00 | First failed login attempt detected |
| 08:12 | 6 failed logins within 3 minutes |
| 08:12 | Successful login after failures |
| 08:30 | Suspicious process executed |

---

## Investigation Steps

1. Searched Splunk for all events related to affected user and host
2. Correlated failed logins with successful login
3. Identified suspicious process execution post-login
4. Checked source IP against threat intelligence
5. Reviewed lateral movement indicators

---

## Findings

- Source IP `185.220.101.34` is external and flagged as malicious
- Account `jsmith` logged in successfully after 6 failed attempts
- Post-login PowerShell execution with encoded command detected
- Likely credential compromise and malware execution

---

## MITRE ATT&CK Mapping

| Technique ID | Technique Name | Evidence |
|---|---|---|
| T1110 | Brute Force | 6 failed logins before success |
| T1059.001 | PowerShell | Encoded PowerShell executed post-login |
| T1027 | Obfuscation | -enc flag used in PowerShell |

---

## Decision

- [ ] False Positive — Close ticket
- [x] True Positive — Escalate to Tier 2

**Reason:** External IP, brute force success, malicious PowerShell execution

---

## Containment Actions Taken

- [ ] Source IP blocked at firewall
- [ ] User account disabled
- [ ] Host isolated from network
- [ ] Notified Tier 2 / IR team
- [ ] Evidence preserved

---

## Recommendations

1. Block IP `185.220.101.34` permanently at perimeter firewall
2. Enforce MFA for all remote logins
3. Restrict PowerShell ExecutionPolicy to AllSigned
4. Enable PowerShell ScriptBlock logging
5. Tune SIEM alert threshold for brute force to 3 attempts

---

## Analyst Notes

Add any additional observations, IOCs, or context here.