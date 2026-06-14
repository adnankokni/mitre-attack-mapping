# 🟣 APT Simulation — Full Kill Chain MITRE Mapping

**Scenario:** Nation-state APT conducts long-term espionage operation.
**Based on:** APT28 (Fancy Bear) known TTPs
**Dwell Time:** 47 days before detection

---

## Full Kill Chain Mapping

| Day | Tactic | Technique | Description |
|-----|--------|-----------|-------------|
| 1 | Initial Access | T1566.001 | Spearphishing with zero-day exploit in PDF |
| 1 | Execution | T1203 | Exploitation for Client Execution |
| 2 | Persistence | T1543.003 | Create/Modify System Process: Windows Service |
| 3 | Defence Evasion | T1036.005 | Masquerading: Match Legitimate Name |
| 5 | C2 | T1071.001 | Web Protocols: HTTPS to C2 server |
| 7 | C2 | T1132.001 | Data Encoding: Standard Encoding |
| 14 | Discovery | T1082 | System Information Discovery |
| 14 | Discovery | T1069.002 | Permission Groups: Domain Groups |
| 21 | Credential Access | T1558.003 | Kerberoasting |
| 28 | Lateral Movement | T1021.001 | Remote Desktop Protocol |
| 35 | Collection | T1213 | Data from Information Repositories |
| 42 | Exfiltration | T1048.003 | Exfil Over Alt Protocol: DNS |
| 47 | — | — | **DETECTED by SOC** |

---

## Key Detection Points

| When | What should have caught it | Why it was missed |
|------|--------------------------|-------------------|
| Day 1 | Email gateway — PDF zero-day | Signature not yet available |
| Day 5 | DNS/proxy logs — C2 beaconing | Alert not tuned low enough |
| Day 21 | Kerberoasting detection | Rule not deployed |
| Day 42 | DNS exfiltration | No DNS monitoring in place |

---

## Lessons Learned

1. Deploy Kerberoasting detection rules immediately
2. Enable DNS query logging and monitor for tunnelling
3. Implement network segmentation to limit lateral movement
4. Set up beacon detection for periodic C2 callbacks
5. Hunt proactively — don't wait for alerts
