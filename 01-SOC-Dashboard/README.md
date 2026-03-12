# 01 — SOC Dashboard

## Overview
Built a Splunk SOC Overview dashboard to monitor failed logins,
detect brute force patterns, and identify top alert sources
across endpoint and network log sources.

## Dashboard Panels

| Panel | Purpose | EventCode |
|---|---|---|
| Failed Login Attempts | Detect repeated failed logins | 4625 |
| Brute Force Indicators | Flag accounts with failures then success | 4625 + 4624 |
| Top Alert Sources | Identify noisiest hosts | All |

## Screenshots
See `/screenshots/soc-overview.png`

## Queries
See `/queries/dashboard_queries.spl`

## Key Findings
- Identified accounts with repeated failed logins
- Flagged potential brute force attempts
- Highlighted top hosts generating most events