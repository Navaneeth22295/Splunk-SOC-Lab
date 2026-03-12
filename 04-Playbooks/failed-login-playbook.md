# Playbook: Failed Login / Brute Force Alert

**Trigger:** 5+ failed logins for the same account within 10 minutes  
**Severity:** High / Critical  
**Tactic:** Credential Access — T1110  

---

## Step 1 — Triage

Run in Splunk:
```spl
index=* (sourcetype=WinEventLog EventCode=4625) OR (sourcetype=linux_secure "Failed password")
| rex field=_raw "(?:Account_Name=|for (?:invalid user )?)(?<user>\w+)"
| rex field=_raw "(?:src_ip=|from )(?<src_ip>[\d\.]+)"
| stats count by user, src_ip, sourcetype
| where count > 5
| sort -count
```

**Ask:**
- Is the source IP internal or external?
- Is the account a real user or service account?
- Is the time outside business hours?
- Has the account been locked out?

---

## Step 2 — Investigate

Check if login eventually succeeded:
```spl
index=* sourcetype=WinEventLog (EventCode=4625 OR EventCode=4624)
| stats count(eval(EventCode=4625)) as failures,
        count(eval(EventCode=4624)) as successes by Account_Name, src_ip
| where failures > 5 AND successes > 0
```

---

## Step 3 — Decision

| Condition | Action |
|---|---|
| External IP + off hours + success after failures | Escalate to Tier 2 immediately |
| External IP + no success | Block IP at firewall, monitor |
| Internal IP + known user + business hours | False positive, document and close |
| Service account + locked out | Reset account, notify IT team |

---

## Step 4 — Containment

- Block attacker IP at firewall
- Lock compromised account
- Force password reset
- Notify user and manager

---

## Step 5 — Document

- [ ] Timeline of events recorded
- [ ] Source IP logged
- [ ] Decision made and reason noted
- [ ] Ticket closed or escalated
- [ ] SIEM tuning recommendation added if false positive