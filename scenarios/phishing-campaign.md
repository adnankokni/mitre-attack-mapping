# 🟠 Phishing Campaign — MITRE ATT&CK Mapping

**Scenario:** Credential harvesting phishing campaign targeting finance team.
**Objective:** Steal VPN credentials for initial access.

---

## Attack Chain — MITRE Mapping

| Phase | Tactic | Technique ID | Technique Name | What Happened |
|-------|--------|-------------|----------------|---------------|
| 1 | Reconnaissance | T1598.003 | Phishing for Info: Spearphishing Link | Attacker researched targets on LinkedIn |
| 2 | Resource Dev | T1583.001 | Acquire Infrastructure: Domains | Registered paypa1-secure.com |
| 3 | Initial Access | T1566.002 | Phishing: Spearphishing Link | Email with fake PayPal login link sent |
| 4 | Credential Access | T1056.003 | Input Capture: Web Portal Capture | Fake login page captured credentials |
| 5 | Initial Access | T1078 | Valid Accounts | Stolen creds used to log into VPN |
| 6 | Discovery | T1087.002 | Account Discovery: Domain Account | Attacker enumerated AD users |
| 7 | Persistence | T1136.001 | Create Account: Local Account | New admin account created |

---

## Detection Opportunities

| Technique | Detection Method | Priority |
|-----------|-----------------|---------|
| T1566.002 | Email gateway: Check SPF/DKIM/DMARC failures | High |
| T1583.001 | Threat intel: Monitor newly registered look-alike domains | Medium |
| T1078 | SIEM: Login from new IP/country after credential theft | High |
| T1087.002 | AD logs: LDAP queries for user enumeration | Medium |
| T1136.001 | Windows Event 4720: New user account created | High |

---

## Email Header Analysis Checklist

- [ ] SPF record passes?
- [ ] DKIM signature valid?
- [ ] DMARC policy enforced?
- [ ] Reply-To matches From address?
- [ ] Domain registered recently (< 30 days)?
- [ ] URL uses HTTP instead of HTTPS?
- [ ] URL contains IP address instead of domain?
