# 03 — Threat Detection & MITRE ATT&CK Mapping

## Overview
Mapped all detections from log analysis to MITRE ATT&CK
tactics and techniques. Identified 8 distinct attack
behaviors across Credential Access, Execution, Persistence,
Privilege Escalation, and Defense Evasion tactics.

## Tactics Covered

| Tactic | Count |
|---|---|
| Credential Access | 1 |
| Execution | 3 |
| Persistence | 2 |
| Privilege Escalation | 1 |
| Defense Evasion | 2 |

## Most Critical Findings
- Backdoor account creation (T1136)
- Reverse shell via cron (T1053)
- PowerShell download cradle (T1059.001)

## See Also
- `mitre-mapping.md` — Full mapping table and attack timeline
- `queries/threat_queries.spl` — All SPL detection queries
- `screenshots/` — Splunk search results