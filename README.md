# ⚔️ MITRE ATT&CK Mapping Project — SOC Analyst Portfolio

![MITRE](https://img.shields.io/badge/MITRE-ATT%26CK_v14-red?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)
![Techniques](https://img.shields.io/badge/Techniques_Mapped-25+-orange?style=flat-square)
![Scenarios](https://img.shields.io/badge/Scenarios-4-blue?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)

A professional MITRE ATT&CK mapping project demonstrating how a SOC analyst
maps real-world attack scenarios to specific adversary tactics and techniques,
builds detection rules, and analyses threat actor TTPs.

---

## 🎯 What This Project Demonstrates

- Mapping real attack chains to MITRE ATT&CK tactics and techniques
- Building detection rules (Sigma + Wazuh) for specific techniques
- Analysing known APT group TTPs (APT28, Lazarus Group)
- Using the ATT&CK Navigator to visualise coverage
- Understanding the full adversary kill chain

---

## 📁 Repository Structure

```
mitre-attack-mapping/
├── scenarios/              # Attack scenarios with full MITRE mapping
│   ├── ransomware-attack.md
│   ├── phishing-campaign.md
│   ├── lateral-movement.md
│   └── apt-simulation.md
├── techniques/             # Deep-dive on individual techniques
│   ├── T1566-phishing.md
│   ├── T1078-valid-accounts.md
│   ├── T1110-brute-force.md
│   └── T1486-data-encrypted.md
├── detections/             # Detection rules per technique
│   ├── sigma-rules/
│   └── wazuh-rules/
├── navigator/              # ATT&CK Navigator layer files
│   └── attack-layer.json
└── threat-actors/          # Known APT TTP analysis
    ├── APT28.md
    └── Lazarus-Group.md
```

---

## ⚔️ Attack Scenarios Mapped

| Scenario | Techniques Mapped | Tactics Covered |
|----------|------------------|----------------|
| [Ransomware Attack Chain](scenarios/ransomware-attack.md) | 11 | Initial Access → Impact |
| [Phishing Campaign](scenarios/phishing-campaign.md) | 7 | Reconnaissance → Persistence |
| [Lateral Movement](scenarios/lateral-movement.md) | 8 | Discovery → Collection |
| [APT Simulation](scenarios/apt-simulation.md) | 14 | Full Kill Chain |

---

## 🗺️ ATT&CK Navigator Heatmap

The `navigator/attack-layer.json` file can be loaded directly into the
[MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator)
to visualise all mapped techniques.

**Colour coding:**
- 🔴 Red — Confirmed technique observed
- 🟠 Orange — Suspected/likely technique
- 🟢 Green — Detection rule exists

---

## 🔍 Detection Rules Built

| Rule | Technique | Type | Severity |
|------|-----------|------|---------|
| Encoded PowerShell | T1059.001 | Sigma + Wazuh | High |
| SSH Brute Force | T1110 | Sigma + Wazuh | Medium |
| New User Created | T1136 | Wazuh | Medium |
| Shadow Copy Deletion | T1490 | Wazuh | Critical |
| Sudo Escalation | T1548.003 | Wazuh | High |

---

## 🕵️ Threat Actors Analysed

| Actor | Origin | Motivation | Key Techniques |
|-------|--------|-----------|---------------|
| [APT28](threat-actors/APT28.md) | Russia | Espionage | T1566, T1071, T1003 |
| [Lazarus Group](threat-actors/Lazarus-Group.md) | North Korea | Financial/Espionage | T1486, T1041, T1059 |

---

## 🧠 Key Skills Demonstrated

- MITRE ATT&CK framework (v14) — Enterprise matrix
- Adversary TTP analysis and kill chain mapping
- Sigma rule writing for cross-platform detection
- Wazuh SIEM rule development with MITRE tagging
- ATT&CK Navigator usage and layer creation
- Threat actor profiling and TTP documentation

---

## 🔗 Related Portfolio Projects

- [Incident Response Playbook](https://github.com/adnankokni/incident-response-playbook)

---

## 📚 References

- [MITRE ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/)
- [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator)
- [Sigma Rules Repository](https://github.com/SigmaHQ/sigma)
- [MITRE ATT&CK for SOC Analysts](https://attack.mitre.org/resources/getting-started/)

---

*Part of my SOC Analyst portfolio. All scenarios are based on publicly
documented attacks and used for educational purposes only.*
