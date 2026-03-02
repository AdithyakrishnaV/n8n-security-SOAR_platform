# Playbook 1 — IP Reputation Checker
## The Problem:
Someone reports a suspicious IP address
        ↓
Analyst manually checks VirusTotal
        ↓
Then manually checks AbuseIPDB
        ↓
Then manually calculates if it's dangerous
        ↓
Takes 20 minutes per IP
        ↓
100 IPs per day = impossible to keep up
## With This Playbook:
Suspicious IP reported via webhook
        ↓
VirusTotal checks it against 93 security engines
        ↓
AbuseIPDB checks community abuse reports
        ↓
Risk score calculated automatically
        ↓
Discord alert if dangerous
        ↓
All in 10 seconds, zero humans needed

## Real World Use:
Every time a server logs a connection from an unknown IP, it sends that IP to this workflow. Your SOC team wakes up to a prioritized list of only the dangerous ones — not 10,000 raw logs.

# Playbook 2 — Brute Force Detection
## The Problem:
Hacker hammers your SSH server with 500 password attempts
        ↓
Server logs fill up with failed login entries
        ↓
Analyst has to manually review logs
        ↓
By the time they notice, hacker already got in
        ↓
Average time to detect: 18 hours
## With This Playbook:
Server detects 10+ failed logins in 30 seconds
        ↓
Automatically sends alert to n8n webhook
        ↓
Attacker IP checked against threat feeds
        ↓
Attack velocity calculated (attempts per minute)
        ↓
Admin account targeted = higher risk score
        ↓
CRITICAL alert fires in Discord in under 60 seconds
        ↓
Analyst blocks the IP before attacker succeeds

## Real World Use:
Connects to fail2ban on your Linux servers. The moment an attack starts, your team knows about it with full context — not just a log entry but a complete threat profile of who is attacking and how dangerous they are.

# Playbook 3 — Phishing Email Triage
## The Problem:
Employee forwards suspicious email to security team
        ↓
Analyst opens the email carefully
        ↓
Manually copies each URL into VirusTotal
        ↓
Manually checks sender IP
        ↓
Manually writes up findings in a ticket
        ↓
Takes 30-45 minutes per email
        ↓
Company gets 50 reported emails per day
        ↓
Team is completely overwhelmed
## With This Playbook:
Employee forwards suspicious email to abuse@company.com
        ↓
Email automatically sent to n8n webhook
        ↓
Every URL extracted from email body automatically
        ↓
Each URL checked against VirusTotal simultaneously
        ↓
Sender IP checked against AbuseIPDB
        ↓
Sender domain checked for suspicious TLD (.ru .xyz .tk)
        ↓
Risk score calculated from all sources combined
        ↓
Discord alert with full evidence report
        ↓
All in under 30 seconds
## Real World Use:
Security teams at banks, hospitals, and enterprises deal with hundreds of phishing emails daily. This workflow lets one analyst handle what used to require a team of five. The ones that score LOW get auto-closed. Only HIGH and CRITICAL need human eyes.

# Playbook 4 — Threat Intel Feed (scanner)
## The Problem:
Hackers create new malicious domains and IPs every day
        ↓
Your firewall blocklist is updated weekly at best
        ↓
5 day gap where employees can reach malicious sites
        ↓
Threat intel feeds cost $50,000+ per year
        ↓
Small companies just go without
        ↓
Get compromised
## With This Playbook:
Every 4 hours automatically wakes up
        ↓
Fetches latest IOCs from AlienVault OTX (free)
        ↓
Fetches active malware URLs from Abuse.ch (free)
        ↓
Combines and deduplicates everything
        ↓
Saves unified watchlist
        ↓
Discord report of what's new
        ↓
All other playbooks automatically use fresh data
## Real World Use:
Enterprise SOCs pay Recorded Future or CrowdStrike $100k+/year for this. You're doing the same thing with free OSINT feeds. The watchlist this generates feeds directly into your firewall rules and SIEM detection logic.

# Playbook 5 — Vulnerability Management 
## The Problem:
Security scanner finds 847 vulnerabilities across your servers
        ↓
All marked as "High" or "Critical"
        ↓
IT team asks which one to fix first
        ↓
Analyst manually looks up each CVE
        ↓
Manually checks if exploit exists in the wild
        ↓
Manually creates JIRA tickets for each one
        ↓
Takes days, meanwhile attackers exploit the gap
## With This Playbook:

Webhook (receives scanner results)
        ↓
HTTP Request (fetches 1,529 CISA KEV vulnerabilities)
        ↓
Code JS1 (matches your CVEs against KEV database)
        ↓
Code JS2 (calculates priority score for each CVE)
        ↓
IF (filters — only score 70+ gets actioned)
        ↓
Jira (creates tickets automatically — SCRUM-5, 6, 7)
        ↓
Discord (alerts team with full threat report)


Vulnerability scanner sends results to n8n
        ↓
Each CVE looked up automatically
        ↓
Checks if active exploit exists in the wild
        ↓
Cross references with CISA Known Exploited Vulnerabilities
        ↓
Prioritizes by real world risk, not just CVSS score
        ↓
Creates JIRA tickets automatically with patch instructions
        ↓
Patches the most dangerous ones first
## Real World Use:
A hospital with 500 servers cannot patch everything at once. This workflow tells the IT team exactly which 5 vulnerabilities will get them hacked this week and creates the work tickets automatically.

# Playbook 6 — Executive Dashboard
## The Problem:
CISO walks into board meeting
        ↓
Board asks "how secure are we?"
        ↓
CISO has no real time numbers
        ↓
Manually pulls data from 6 different tools
        ↓
Spends 4 hours building a PowerPoint
        ↓
Data is already outdated by the time it's presented
## With This Playbook:
Every Monday morning automatically
        ↓
Counts all incidents from the past week
        ↓
Calculates MTTR (how fast did we respond?)
        ↓
Calculates MTTD (how fast did we detect?)
        ↓
Shows top threat types and trends
        ↓
Generates HTML report automatically
        ↓
Emails it to leadership before they wake up
## Real World Use:
Every security team needs to prove their value to the business. This workflow generates the numbers that justify the security budget and shows the board that the SOC is working.

# The Big Picture — How All 6 Connect
Playbook 4 (Threat Intel)
    ↓ feeds watchlist to
Playbook 1 (IP Checker) ←── any suspicious IP anywhere
Playbook 2 (Brute Force) ←── server attack alerts
Playbook 3 (Phishing) ←── reported emails
    ↓ all incidents feed into
Playbook 5 (Vuln Management) ←── scanner results
    ↓ all data feeds into
Playbook 6 (Dashboard) ←── weekly report to leadership