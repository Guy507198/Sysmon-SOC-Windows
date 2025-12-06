# Attacks – Simulation d’activités malveillantes sur l’hôte Windows

Ce dossier rassemble l’ensemble des tests d’attaque réalisés sur la machine Windows dédiée au projet Sysmon-SOC.
L’objectif est de générer différents comportements typiques observés lors d’intrusions : création de fichiers, exécution PowerShell obfusquée, reconnaissance locale, accès au registre et utilisation d’EncodedCommand.

---

## 1. Création et suppression d’un fichier suspect  
**Image :** `file-creation-test.png`  
Création puis suppression rapide d’un fichier *malicious.txt* dans *C:\Users\Public*.  
Ce comportement imite les scripts malveillants déposant des fichiers temporaires.

---

## 2. Exécution PowerShell obfusquée  
**Image :** `powershell-obfuscated.png`  
Commande exécutée avec :  
`powershell.exe -nop -w hidden -c "IEX('test')"`  
Technique souvent utilisée pour masquer l’exécution d’un script.

---

## 3. Reconnaissance locale de l’hôte  
**Image :** `reconnaissance-commands.png`  
Contient :  
- ipconfig /all  
- net user  
- net localgroup Administrateurs  
- whoami /all  
Représente la collecte d’informations système par un attaquant.

---

## 4. Consultation du registre Windows  
**Image :** `registry-access-test.png`  
Commande :  
`reg query HKLM\Software`  
Utilisée pour extraire des informations système sensibles.

---

## 5. Exécution PowerShell EncodedCommand  
**Image :** `test.png`  
Payload encodé en Base64 exécuté via :  
`powershell.exe -enc <Base64>`  
Déclenche la détection Sentinel correspondant à MITRE T1059.

---

## Résumé des fichiers inclus

| Fichier | Description |
|--------|-------------|
| file-creation-test.png | Création/suppression de fichier suspect |
| powershell-obfuscated.png | Commande PowerShell obfusquée |
| reconnaissance-commands.png | Commandes de reconnaissance |
| registry-access-test.png | Accès registre Windows |
| test.png | EncodedCommand Base64 |

