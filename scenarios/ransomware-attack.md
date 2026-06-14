# 🔴 Ransomware Attack — MITRE ATT&CK Mapping

**Scenario:** A threat actor gains initial access via a phishing email,
establishes persistence, moves laterally, and deploys ransomware.

**Threat Actor Profile:** Financially motivated cybercriminal group
**Target:** Mid-size enterprise, Windows environment

---

## Attack Chain — Full MITRE Mapping

| Phase | Tactic | Technique ID | Technique Name | What Happened |
|-------|--------|-------------|----------------|---------------|
| 1 | Initial Access | T1566.001 | Phishing: Spearphishing Attachment | Victim opened malicious Word doc |
| 2 | Execution | T1204.002 | User Execution: Malicious File | Macro executed PowerShell payload |
| 3 | Execution | T1059.001 | Command & Scripting: PowerShell | PowerShell downloaded second stage |
| 4 | Persistence | T1547.001 | Boot/Logon Autostart: Registry Run Keys | Malware added to HKCU Run key |
| 5 | Defence Evasion | T1562.001 | Impair Defences: Disable AV | Windows Defender disabled via GPO |
| 6 | Credential Access | T1003.001 | OS Credential Dumping: LSASS Memory | Mimikatz dumped credentials |
| 7 | Lateral Movement | T1550.002 | Use Alternate Auth: Pass the Hash | Admin hash used to access file server |
| 8 | Discovery | T1083 | File and Directory Discovery | Attacker searched for valuable files |
| 9 | Collection | T1005 | Data from Local System | Documents staged for encryption |
| 10 | Impact | T1486 | Data Encrypted for Impact | Files encrypted, ransom note dropped |
| 11 | Impact | T1490 | Inhibit System Recovery | Shadow copies deleted via vssadmin |

---

## Detection Opportunities

| Technique | Log Source | What to Look For |
|-----------|-----------|-----------------|
| T1566.001 | Email gateway | Attachments with macros from external senders |
| T1059.001 | Windows Event 4104 | PowerShell script block logging, encoded commands |
| T1547.001 | Windows Registry | New entries in HKCU\Software\Microsoft\Windows\CurrentVersion\Run |
| T1562.001 | Windows Event 7045 | AV service stopped, new service installed |
| T1003.001 | Windows Event 4656 | LSASS process accessed by non-system process |
| T1550.002 | Windows Event 4624 | Logon Type 3 with NTLM from new source |
| T1486 | File system / Wazuh FIM | Mass file modification events in short timeframe |
| T1490 | Windows Event 524 | Shadow copy deletion detected |

---

## Wazuh Detection Rules

```xml


  60910
  
    (?i)powershell.*(-enc|-encodedcommand|-e\s)
  
  MITRE T1059.001: Encoded PowerShell command detected
  
    T1059.001
  




  60910
  
    (?i)vssadmin.*delete.*shadows
  
  MITRE T1490: Shadow copy deletion — Ransomware indicator
  
    T1490
  

```

---

## Recommendations

1. Enable PowerShell Script Block Logging (Event ID 4104)
2. Deploy application allowlisting to block macro execution
3. Implement LSASS protection (Windows Credential Guard)
4. Enforce MFA to prevent pass-the-hash success
5. Maintain offline backups to recover from T1486
6. Deploy Wazuh FIM on critical directories
