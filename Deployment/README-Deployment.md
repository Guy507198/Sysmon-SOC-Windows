# README – Deployment (Sysmon-SOC-Windows)

Ce dossier regroupe l’ensemble des étapes nécessaires au déploiement d’un environnement Windows instrumenté pour l’analyse de sécurité, incluant l’installation de Sysmon, la configuration des politiques d’audit, l’activation de la journalisation avancée, et l’intégration avec Azure via AMA et Azure Arc.  
Chaque image illustre une phase précise du déploiement, depuis l’installation de la machine jusqu’à la connexion aux services Azure.

---

## 1. Préparation de la machine Windows

### windows-installed.png
Capture de l’environnement Windows fraîchement installé, servant de base à la configuration Sysmon + AMA.

---

## 2. Configuration des politiques d’audit Windows

### audit-policy.png
Activation des stratégies d’audit avancées (processus, accès au registre, politique d’authentification…).  
Ces paramètres permettent de générer des journaux de sécurité exploitables par Sysmon et Azure Monitor.

---

## 3. Activation des logs PowerShell

### ps-transcription.png
Mise en place de la transcription PowerShell, permettant d’enregistrer toutes les commandes exécutées.

### script-block-logging.png
Activation de la journalisation ScriptBlock, essentielle pour détecter du code PowerShell obfusqué ou injecté.

### module-logging.png
Capture montrant la journalisation des modules PowerShell chargés.

---

## 4. Configuration avancée des journaux Windows

### security-log-check.png
Capture des journaux de sécurité après activation de toutes les politiques nécessaires.

### commandline-audit-registry.png
Vérification des paramètres de journalisation de la ligne de commande et des accès au registre.

---

## 5. Installation et enrôlement Azure via ARC

### arc-generation-script.png
Script de génération Azure Arc permettant l’intégration de la machine Windows dans Azure.

### azure-arc-script-execution.png
Exécution du script d’enrôlement Azure Arc dans PowerShell.

### azure-arc-machine-connected.png
Confirmation de la connexion de la VM via Azure Arc.

---

## 6. Installation de l’agent AMA (Azure Monitor Agent)

### ama-extension-installed.png
Déploiement réussi de l’extension Azure Monitor Agent.

### ama-service-running.png
Vérification du bon fonctionnement du service AMA.

---

## 7. Association aux Data Collection Rules (DCR)

### dcr-add-resource.png
Ajout de la ressource Windows comme source dans la DCR Sysmon/Windows Events.

### dcr-sysmon-added.png
Confirmation de la prise en charge des événements Sysmon.

### dcr-windows-eventlogs.png
Routage des journaux Windows natifs (Security, System, PowerShell).

---

## 8. Configuration réseau dans la VM

### vm-network-mode.png
Paramétrage du mode réseau de la VM pour supporter l’architecture SOC.

---

## Résumé du déploiement

Le dossier Deployment contient toutes les étapes essentielles pour construire la chaîne :

Windows → Sysmon → AMA → DCR → Log Analytics → Sentinel

---

