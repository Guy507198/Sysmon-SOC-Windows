# Windows SOC – Azure Sentinel & Sysmon Monitoring

## 1. Objectif du Projet
Mettre en place une architecture SOC Windows complète : Sentinel, Log Analytics, AMA, DCR, Sysmon, KQL, règles MITRE.

## 2. Architecture Globale
- RG-Sysmon-SOC
- LAW-Sysmon-SOC
- Microsoft Sentinel
- VM Win11-SOC + Sysmon + AMA

## 3. Installation Sysmon
```
.\sysmon64.exe -i sysmonconfig-export.xml
Get-Service Sysmon64
```

## 4. Azure Monitor Agent + Data Collection Rule
DCR-WindowsSysmon → collecte Sysmon + Journaux Windows vers LAW.

## 5. Vérifications KQL
### Process Create
```
Event
| where EventLog == "Microsoft-Windows-Sysmon/Operational"
| where EventID == 1
| take 20
```

### Network Connection
```
Event
| where EventID == 3
| take 20
```

## 6. Attaques Simulées
- File Creation (EventID 11)
- Encoded PowerShell (MITRE T1059)
- Reconnaissance (ipconfig, whoami, reg query)

## 7. Analytic Rule MITRE T1059
Détection de commandes PowerShell obfusquées.

## 8. Conclusion
Pipeline complet opérationnel : ingestion → analyse → détection → alertes.

## 9. Arborescence
```
Sysmon-SOC-Windows/
├── Architecture/
├── Sysmon/
├── Attacks/
├── KQL/
└── Reports/
```
