# 02 — Log Analysis

## Overview
Analyzed Windows Event Logs and Linux syslogs to detect
anomalous behavior including brute force attacks, privilege
abuse, suspicious process execution, and backdoor activity.

## Key Findings

| Finding | Source | Severity |
|---|---|---|
| Brute force SSH from 185.220.101.34 | linux_secure | Critical |
| Backdoor account created by aroberts | linux_secure | Critical |
| PowerShell download cradle by aroberts | WinEventLog | Critical |
| Malicious cron reverse shell | linux_secure | Critical |
| Sudo abuse - chmod 777 /etc/passwd | linux_secure | High |
| Multiple failed logins - jsmith | WinEventLog | High |

## Attacker IPs Identified
- `185.220.101.34` — External, multiple attacks
- `203.0.113.50` — External, SSH brute force
- `10.0.0.45` — Internal, suspicious activity

## Screenshots
See `/screenshots/` folder for all search results.

## Queries
See `/queries/detection_queries.spl`