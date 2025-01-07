# EKOLOCLAST
Projet 3

# 🌐 **Plan de projet réseau pour Ekoloclast**

---

## 🔍 **1. Analyse des besoins et contraintes**

### 🏢 **Entreprise : Ekoloclast**
- **Localisation** : Paris, 20ème arrondissement.
- **Effectif** : 183 employés répartis en 10 départements.
- **Objectif** : Révolutionner l'approche écologique (B2B et B2C).
- **Fusion prévue** : Préparation nécessaire à une intégration future.

### 🚧 **Contraintes techniques actuelles**
- Réseau Wi-Fi basique (box FAI, répéteurs, mot de passe faible).
- Pas de serveur dédié ni de sécurité réseau.
- Stockage local sur les machines.
- Messagerie hébergée dans le cloud.
- Nomadisme partiel pour le département commercial.

### 🎯 **Objectifs principaux**
- Mise en place d'une infrastructure réseau sécurisée et scalable.
- Gestion centralisée des services et données.
- Préparation pour une organisation fusionnée.

---

## 📅 **2. Proposition de répartition des objectifs par sprint**

| **Sprint**  | **Objectifs principaux**                                                                                 | **Objectifs secondaires**                                              | **Optionnels**                              |
|-------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|--------------------------------------------|
| **Semaine 1** | Étude des besoins. Schéma réseau prévisionnel. Plan d'adressage IP. Choix du matériel réseau.             | Convention de nommage. Choix des VLANs.                               | -                                            |
| **Semaine 2** | Installation des routeurs/switches. Création des VLANs. Configuration du routage.                        | Installation des points d'accès Wi-Fi.                                | -                                            |
| **Semaine 3** | Mise en place des serveurs (AD, DNS, DHCP). Configuration des droits d’accès.                            | Configuration de la messagerie interne (Exchange).                    | Intégration SSO avec messagerie cloud.      |
| **Semaine 4** | Configuration du réseau Wi-Fi sécurisé (SSID par VLAN). Déploiement des solutions de sécurité (Firewall). | Mise en place des sauvegardes (NAS ou Cloud).                         | Surveillance du réseau via Zabbix/PRTG.     |
| **Semaine 5** | Formation des utilisateurs. Documentation complète.                                                     | Tests de redondance réseau et de sauvegarde.                          | Préparation à l’intégration d'une autre entité. |

---

## 🖥️ **3. Schéma réseau prévisionnel**

### 📋 **Matériel nécessaire**

| **Équipement**                | **Quantité estimée** | **Remarques**                                                                                     |
|-------------------------------|----------------------|--------------------------------------------------------------------------------------------------|
| Routeurs                      | 2                    | 1 principal et 1 pour la redondance.                                                             |
| Switches (manageable)         | 5                    | Un par zone avec support VLAN.                                                                   |
| Points d’accès Wi-Fi          | 10                   | Couverture homogène et support pour plusieurs SSID.                                              |
| Serveurs physiques            | 3                    | AD/DNS, DHCP, NAS/sauvegarde.                                                                   |
| Onduleurs (UPS)               | 3                    | Protection contre les coupures de courant.                                                       |
| Firewall matériel             | 1                    | Sécurité réseau avec gestion des menaces (ex. FortiGate).                                        |
| Licences Windows Server       | 3                    | Pour les serveurs AD, DNS, DHCP.                                                                 |

### 🛠️ **Architecture**
- **VLANs** pour isolation des départements :
  - VLAN 10 : Direction Générale.
  - VLAN 20 : Direction Marketing.
  - VLAN 30 : RH.
  - VLAN 40 : Commercial nomade.
  - VLAN 50 : Invités (Wi-Fi public séparé).
- **Plan d’adressage IP** (192.168.X.0/24 pour chaque VLAN).
- **Routeur central** pour gérer le routage inter-VLAN.

---

## 📝 **4. Convention de nommage**

- **Postes utilisateurs :** `PC-<Département>-<NomUtilisateur>`
  - Exemple : `PC-DSI-JDupont`.
- **Serveurs :** `SRV-<Fonction>`
  - Exemple : `SRV-AD`, `SRV-DHCP`.
- **Switches :** `SW-<Étage>`
  - Exemple : `SW-1`, `SW-2`.
- **Routeurs :** `RTR-<NomZone>`
  - Exemple : `RTR-MAIN`, `RTR-BACKUP`.

---

## 🎯 **5. Objectifs détaillés**

### 🔒 **1. JOURNALISATION - Gestion des logs centralisée**
1. Utilisation de l'un des systèmes suivants :
   - [Graylog](https://github.com/Graylog2/graylog2-server).
   - [Syslog-ng](https://github.com/syslog-ng/syslog-ng).
2. Mise en production :
   - Installation sur VM (non-dédié) ou CT.
   - Gestion des logs des serveurs.

### 🛡️ **2. JOURNALISATION - Logs des scripts PowerShell**
1. Les logs seront construits pour pouvoir être lus par l'un des systèmes suivants :
   - Observateur d’événements Windows.
   - [CMTRACE](https://www.tech2tech.fr/cmtrace-lire-vos-fichiers-logs-facilement/).
2. Gestion des logs :
   - Modifier ou ajouter cette gestion de logs dans les scripts PowerShell utilisés (actuels et à venir).
   - Utiliser un répertoire spécifique pour les logs (à définir).
   - Un seul log par script.

### 🖥️ **3. SUPERVISION - Infrastructure réseau**
1. Utilisation d'au moins un des logiciels suivants :
   - [ZABBIX](https://www.zabbix.com/).
   - [M/MONIT](https://mmonit.com/).
   - [PRTG](https://www.paessler.com/).
   - [NAGIOS Core](https://www.nagios.org/projects/nagios-core/).
2. Mise en production :
   - Installation sur VM/CT dédié.
   - Supervision des éléments de l'infrastructure (actuels et à venir).
   - Mise en place de dashboards.

### 🔍 **4. SUPERVISION - Surveillance du pare-feu pfsense**
1. Mise en place de dashboards.
2. Ajout et modification de widgets.

### 👩‍💼 **5. AD - Fichier RH**
1. Intégration des nouveaux utilisateurs.
2. Modifications des informations suivantes :
   - Le département "R&D" devient "Recherche et Innovation".
   - Le service "Formation" est rattaché au département "DSI".
   - Le département "Services Généraux" devient "Gestion des biens" avec :
     - Jean-Pascal Millith, "Responsable Département Gestion des biens".
   - Le service "Santé et Sécurité au travail" devient "QHSE" avec :
     - Sandra Lorient, nouvelle responsable.
     - Les techniciens HSE renommés "Techniciens QHSE".
   - Gestion des changements de noms liés aux mariages/divorces.

---

## 📦 **6. Contexte et réflexion**

### 📈 **Évolution de l'entreprise**
Une entreprise est en perpétuel mouvement. Pour suivre les changements :
- Gérer dynamiquement les utilisateurs (arrivées/départs).
- Réfléchir aux meilleurs moyens de maintenir les informations RH à jour.

### 📖 **Documentation requise**
- **Prérequis matériel/logiciel :**
  - Versions d'OS, logiciels utilisés.
- **Installation :**
  - Instructions pas-à-pas avec copies d'écran.
- **Configuration/Utilisation :**
  - Guides détaillés et FAQ.

---

## ✅ **Conclusion**
Chaque composant est optimisé pour répondre aux exigences actuelles et futures d’Ekoloclast.
