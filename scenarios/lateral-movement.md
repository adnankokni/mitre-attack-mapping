# 🔵 Lateral Movement — MITRE ATT&CK Mapping

**Scenario:** Attacker with foothold on workstation moves laterally
to domain controller and file servers.

---

## Attack Chain — MITRE Mapping

| Phase | Tactic | Technique ID | Technique Name | What Happened |
|-------|--------|-------------|----------------|---------------|
| 1 | Discovery | T1016 | System Network Configuration Discovery | ipconfig /all run on victim |
| 2 | Discovery | T1018 | Remote System Discovery | net view, ping sweep performed |
| 3 | Discovery | T1049 | System Network Connections | netstat -an to find active sessions |
| 4 | Credential Access | T1003.001 | LSASS Memory Dump | Mimikatz harvested domain admin hash |
| 5 | Lateral Movement | T1021.001 | Remote Services: RDP | Used stolen creds to RDP to file server |
| 6 | Lateral Movement | T1550.002 | Pass the Hash | PTH attack against domain controller |
| 7 | Lateral Movement | T1021.002 | SMB/Windows Admin Shares | PsExec used to run commands on DC |
| 8 | Collection | T1039 | Data from Network Shared Drive | Sensitive files copied from file server |

---

## Detection Commands — What Analysts Run

```bash
# Detect RDP connections in Windows Event Logs
# Event ID 4624 with Logon Type 10 = RDP
Get-EventLog -LogName Security -InstanceId 4624 | `
  Where-Object {$_.Message -match "Logon Type.*10"} | `
  Select -First 20

# Detect SMB lateral movement on Linux (Wazuh agent)
sudo grep "smb\|psexec\|admin\$" /var/log/syslog | tail -50

# Detect pass-the-hash (Event ID 4624, logon type 3, NTLM)
Get-WinEvent -FilterHashtable @{
  LogName='Security'; Id=4624
} | Where-Object {
  $_.Message -match "NTLM" -and $_.Message -match "Logon Type.*3"
}
```

---

## Wazuh Detection Rule

```xml


  60910
  
    (?i)psexec|PSEXESVC
  
  MITRE T1021.002: PsExec lateral movement detected
  
    T1021.002
  

```
