# MITRE ATT&CK Threat Mapping

## Environment
- **Log Sources:** Windows Event Logs, Linux Syslogs
- **Analysis Period:** March 10, 2026
- **Tool:** Splunk SIEM
- **Framework:** MITRE ATT&CK v14

---

## Findings

| # | Detection | MITRE Tactic | Technique ID | Technique Name | Severity | Source IP |
|---|---|---|---|---|---|---|
| 1 | Repeated failed logins on Windows & Linux | Credential Access | T1110 | Brute Force | Critical | 185.220.101.34, 203.0.113.50 |
| 2 | PowerShell download cradle executed | Execution | T1059.001 | PowerShell | Critical | Internal |
| 3 | Backdoor account created via useradd | Persistence | T1136.001 | Local Account | Critical | Internal |
| 4 | Reverse shell in cron job | Persistence | T1053.003 | Cron | Critical | 185.220.101.34 |
| 5 | Sudo used to read /etc/shadow | Privilege Escalation | T1548.003 | Sudo and Sudo Caching | High | Internal |
| 6 | chmod 777 on /etc/passwd | Defense Evasion | T1222.002 | File Permissions Modification | High | Internal |
| 7 | Encoded PowerShell (-enc flag) | Defense Evasion | T1027 | Obfuscated Files or Information | High | Internal |
| 8 | curl pipe to bash from cron | Execution | T1059.004 | Unix Shell | Critical | 185.220.101.34 |

---

## Attack Timeline
```
08:00 — Brute force SSH begins from 185.220.101.34 and 203.0.113.50
08:11 — SSH login accepted for navaneeth (possible compromise)
08:30 — SYN flood detected on ports 80 and 443
09:30 — jsmith runs cmd.exe and encoded PowerShell on WORKSTATION-01
10:00 — aroberts SSH login → immediately creates backdoor account
10:05 — aroberts adds backdoor user and sets password
10:30 — Malicious cron reverse shell planted on linux-server-01
12:05 — navaneeth reads /etc/shadow via sudo
15:00 — bthomas runs chmod 777 on /etc/passwd
16:00 — Malicious curl|bash cron job executes
17:30 — jsmith downloads suspicious script via wget
```

---

## Recommended Actions

| Finding | Action |
|---|---|
| Brute force from external IPs | Block 185.220.101.34 and 203.0.113.50 at firewall |
| Backdoor account created | Disable and remove backdoor account immediately |
| Malicious cron jobs | Audit and remove all unauthorized cron entries |
| PowerShell abuse | Enable PowerShell logging, restrict ExecutionPolicy |
| /etc/passwd permissions | Restore correct permissions immediately |
| /etc/shadow access | Audit all sudo logs, rotate credentials |