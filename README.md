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

| **Sprint**    | **Objectifs principaux**                                                                 | **Objectifs secondaires**                                          | **Optionnels**                           |
|---------------|------------------------------------------------------------------------------------------|----------------------------------------------------------------------|-------------------------------------------|
| **Semaine 1** | Étude des besoins. Schéma réseau prévisionnel. Plan d'adressage IP. Choix du matériel.    | Convention de nommage. Choix des VLANs.                             | -                                         |
| **Semaine 2** | Installation des routeurs/switches. Création des VLANs. Configuration du routage.         | Installation des points d'accès Wi-Fi.                              | -                                         |
| **Semaine 3** | Mise en place des serveurs (AD, DNS, DHCP). Configuration des droits d’accès.             | Configuration de la messagerie interne (Exchange).                  | Intégration SSO avec messagerie cloud.   |
| **Semaine 4** | Configuration du réseau Wi-Fi sécurisé. Déploiement des solutions de sécurité (Firewall). | Mise en place des sauvegardes (NAS ou Cloud).                       | Surveillance réseau via Zabbix/PRTG.     |
| **Semaine 5** | Formation des utilisateurs. Documentation complète.                                      | Tests de redondance réseau et de sauvegarde.                        | Préparation à l’intégration future.      |
| **Semaine 6** | Mise en place des GPO (stratégies de sécurité et standards).                             | Test des scripts et documentation.                                  | Ajout d'options de redondance serveurs.  |
| **Semaine 7** | Configuration de la supervision réseau avec Zabbix/Nagios.                              | Mise en place des tableaux de bord (dashboards).                    | Intégration avec GLPI et logs centralisés.|
| **Semaine 8** | Test des sauvegardes et restauration. Optimisation des configurations existantes.        | Formation des administrateurs sur les solutions mises en place.     | Implémentation des alertes en temps réel.|
| **Semaine 9** | Surveillance avancée du pare-feu et gestion des logs centralisés.                        | Documentation détaillée des configurations.                         | Amélioration de la redondance réseau.    |
| **Semaine 10**| Gestion des utilisateurs et des objets AD. Planification des mises à jour de sécurité.   | Finalisation des configurations avancées pour les scripts.          | Ajout de solutions pour la gestion des invités.|
| **Semaine 11**| Validation de l'ensemble de l'infrastructure. Tests finaux de robustesse et redondance.  | Livraison et présentation de la documentation finale.               | Transition vers les équipes opérationnelles.|

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

### 📌 **Domaines et OU**
- **Nom de domaine FQDN** : `ekoloclast.[TLD]`
- **OU (Unités Organisationnelles)** :
  - Localisation : NomDépartement (optionnel).
  - Exemple : `paris20-communication`.

### 📌 **Groupes de sécurité**
- Format : `group-[L/G]-[pc/us/fc]-[secteur]`
- Exemple : `group-L-pc-dsi`.

### 📌 **Ordinateurs et équipements**
- **Format des noms :**
  - Nom anglais en capital avec type d'équipement et OS/marque.
  - Numéro, département/fonction, emplacement.
  - Exemple : `server-001-dsi-paris20`.
- **Équipements :**
  - **Smartphone** : `smartphone-001-comm-nomade`.
  - **Serveur** : `server-01-AD-DHCP-DNS-paris20`.
  - **Switch** : `switch-paris20`.
  - **Routeur** : `router-paris20`.
  - **Pare-feu** : `firewall-paris20`.

### 📌 **Utilisateurs**
- Format : `NomPrenom-Département`.
- Exemple : `taiev-ol-comm`.
- Gestion des invités/utilisateurs temporaires à prévoir.
- Homonymes gérés par ajout d’identifiants supplémentaires.

### 📌 **GPO (Group Policy Objects)**
- Format : `cible-stratégie-numéro`.
- Exemple : `mktg-noterminal-001`.

### 📌 **Nom des départements**
| Département                  | Abréviation |
|------------------------------|-------------|
| Communication                | Comm        |
| Direction Financière         | DFin        |
| Direction Générale           | DG          |
| Marketing                    | Mktg        |
| Direction des systèmes d'information | DSI  |
| Recherche et Innovation      | RI          |
| Ressources Humaines          | RH          |
| Gestion des Biens            | GB          |
| Service Juridique            | SJuri       |
| Ventes et Développement      | VDC         |

### 📌 **Convention pour adresses IP**
- Format : `IP-Département-NomPrenom`.
- Exemple : `192.168.2.54-comm-taievolga`.

---

## 🌐 **5. Adressage Société Ekoloclast**

- **Réseau** : `172.24.0.0/16`
- **Gateway** : `172.24.255.254`
- **IP DNS** : `172.24.255.254`

### 🏢 **Départements et étendue réseau**

| **Département**            | **Nbr de Services** | **Nbr de Personnes** | **Adresses Disponibles**           | **Etendue du Réseau**         |
|-----------------------------|---------------------|-----------------------|-------------------------------------|--------------------------------|
| Direction Générale          | -                   | 8                     | 30                                  | 172.24.1.1 → 172.24.1.30       |
| Direction Financière        | 3                   | 14                    | 45                                  | 172.24.2.1 → 172.24.2.45       |
| Direction Marketing         | 4                   | 22                    | 70                                  | 172.24.3.1 → 172.24.3.70       |
| DSI                         | 3                   | 12                    | 45                                  | 172.24.4.1 → 172.24.4.45       |
| Recherche et Innovation     | 2                   | 17                    | 60                                  | 172.24.5.1 → 172.24.5.60       |
| Ressources Humaines         | 4                   | 24                    | 75                                  | 172.24.6.1 → 172.24.6.75       |
| Communication               | 3                   | 20                    | 70                                  | 172.24.7.1 → 172.24.7.70       |
| Gestion des Biens           | 2                   | 12                    | 40                                  | 172.24.8.1 → 172.24.8.40       |
| Service Juridique           | 2                   | 8                     | 30                                  | 172.24.9.1 → 172.24.9.30       |
| Ventes et Développement     | 7                   | 46                    | 150                                 | 172.24.10.1 → 172.24.10.150    |

---

## 🎯 **6. Objectifs détaillés**

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

## 📦 **7. Contexte et réflexion**

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
