# 04 — Incident Response Playbooks

## Overview
Tier 1 SOC playbooks for the most common alert types
detected in this lab. Each playbook covers triage,
investigation, decision making, containment, and documentation.

## Playbooks

| File | Alert Type | Severity |
|---|---|---|
| failed-login-playbook.md | Brute Force / Failed Logins | High / Critical |
| malware-alert-playbook.md | Suspicious Process / PowerShell | Critical |
| investigation-report-template.md | Generic incident report template | All |

## How to Use
1. Alert fires in Splunk
2. Open the matching playbook
3. Follow steps 1 through 5
4. Fill in investigation-report-template.md
5. Escalate or close based on decision matrix