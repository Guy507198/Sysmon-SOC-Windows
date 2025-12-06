# README-KQL.md  
Analyse KQL – Journaux Windows & Sysmon dans Microsoft Sentinel

---

## 1. Introduction

Ce document présente l’ensemble des requêtes KQL utilisées pour valider l’ingestion des journaux Windows et Sysmon dans Azure Log Analytics, ainsi que leur visibilité dans Microsoft Sentinel.  
Les captures associées démontrent la bonne collecte, le parsing, et l’exploitation analytique des événements de sécurité.

Les objectifs :
- Vérifier la réception des logs Windows et Sysmon.  
- Inspecter les événements clés (Process Creation, Network Connections).  
- Extraire des informations enrichies à partir de Sysmon EventData.  
- Confirmer la visibilité dans Sentinel.

---

## 2. Vérification de la réception des journaux Sysmon

### Requête KQL
```
Event
| where EventLog == "Microsoft-Windows-Sysmon/Operational"
| where EventID == 1
| take 1
| project EventData
```

---

## 3. Process Creation (Sysmon EventID 1)

```
Event
| where EventLog == "Microsoft-Windows-Sysmon/Operational"
| where EventID == 1
| project TimeGenerated, Computer, EventID, RenderedDescription
| take 20
```

---

## 4. Connexions réseau (Sysmon EventID 3)

```
Event
| where EventLog == "Microsoft-Windows-Sysmon/Operational"
| where EventID == 3
| extend Raw = tostring(EventData)
| extend
    Image = extract("<Data Name=\"Image\">([^<]+)</Data>", 1, Raw),
    User = extract("<Data Name=\"User\">([^<]+)</Data>", 1, Raw),
    Protocol = extract("<Data Name=\"Protocol\">([^<]+)</Data>", 1, Raw),
    SourceIp = extract("<Data Name=\"SourceIp\">([^<]+)</Data>", 1, Raw),
    SourcePort = extract("<Data Name=\"SourcePort\">([^<]+)</Data>", 1, Raw),
    DestinationIp = extract("<Data Name=\"DestinationIp\">([^<]+)</Data>", 1, Raw),
    DestinationPort = extract("<Data Name=\"DestinationPort\">([^<]+)</Data>", 1, Raw),
    DestinationPortName = extract("<Data Name=\"DestinationPortName\">([^<]+)</Data>", 1, Raw)
| project TimeGenerated, Image, User, Protocol, SourceIp, SourcePort, DestinationIp, DestinationPort, DestinationPortName
| take 20
```

---

## 5. Recherche générale Sysmon

```
search *
| where EventLog == "Microsoft-Windows-Sysmon/Operational"
| take 20
```

---

## 6. Vérification des logs Windows Security

```
Event
| take 20
```

---

## 7. Résumé Sentinel

```
Event
| summarize count() by EventLog, EventLevelName
```

---

## 8. Conclusion

- Les événements Windows & Sysmon sont correctement ingérés.  
- Sysmon enrichit les événements critiques.  
- Le parsing KQL fonctionne parfaitement.  
- Sentinel consomme les logs et permet la détection / investigation SOC.

