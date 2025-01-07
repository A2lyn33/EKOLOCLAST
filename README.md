# EKOLOCLAST
Projet 3

# Objectifs semaine 01

# **Plan de projet réseau pour Ekoloclast**

---

## **1. Analyse des besoins et contraintes**

### **Entreprise : Ekoloclast**
- **Localisation** : Paris, 20ème arrondissement.
- **Effectif** : 183 employés répartis en 10 départements.
- **Objectif** : Révolutionner l'approche écologique (B2B et B2C).
- **Fusion prévue** : Préparation nécessaire à une intégration future.

### **Contraintes techniques actuelles**
- Réseau Wi-Fi basique (box FAI, répéteurs, mot de passe faible).
- Pas de serveur dédié ni de sécurité réseau.
- Stockage local sur les machines.
- Messagerie hébergée dans le cloud.
- Nomadisme partiel pour le département commercial.

### **Objectifs principaux**
- Mise en place d'une infrastructure réseau sécurisée et scalable.
- Gestion centralisée des services et données.
- Préparation pour une organisation fusionnée.

---

## **2. Proposition de répartition des objectifs par sprint**

| **Sprint**  | **Objectifs principaux**                                                                                 | **Objectifs secondaires**                                              | **Optionnels**                              |
|-------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|--------------------------------------------|
| **Semaine 1** | Étude des besoins. Schéma réseau prévisionnel. Plan d'adressage IP. Choix du matériel réseau.             | Convention de nommage. Choix des VLANs.                               | -                                            |
| **Semaine 2** | Installation des routeurs/switches. Création des VLANs. Configuration du routage.                        | Installation des points d'accès Wi-Fi.                                | -                                            |
| **Semaine 3** | Mise en place des serveurs (AD, DNS, DHCP). Configuration des droits d’accès.                            | Configuration de la messagerie interne (Exchange).                    | Intégration SSO avec messagerie cloud.      |
| **Semaine 4** | Configuration du réseau Wi-Fi sécurisé (SSID par VLAN). Déploiement des solutions de sécurité (Firewall). | Mise en place des sauvegardes (NAS ou Cloud).                         | Surveillance du réseau via Zabbix/PRTG.     |
| **Semaine 5** | Formation des utilisateurs. Documentation complète.                                                     | Tests de redondance réseau et de sauvegarde.                          | Préparation à l’intégration d'une autre entité. |

---

## **3. Schéma réseau prévisionnel**

### **Matériel nécessaire**

| **Équipement**                | **Quantité estimée** | **Remarques**                                                                                     |
|-------------------------------|----------------------|--------------------------------------------------------------------------------------------------|
| Routeurs                      | 2                    | 1 principal et 1 pour la redondance.                                                             |
| Switches (manageable)         | 5                    | Un par zone avec support VLAN.                                                                   |
| Points d’accès Wi-Fi          | 10                   | Couverture homogène et support pour plusieurs SSID.                                              |
| Serveurs physiques            | 3                    | AD/DNS, DHCP, NAS/sauvegarde.                                                                   |
| Onduleurs (UPS)               | 3                    | Protection contre les coupures de courant.                                                       |
| Firewall matériel             | 1                    | Sécurité réseau avec gestion des menaces (ex. FortiGate).                                        |
| Licences Windows Server       | 3                    | Pour les serveurs AD, DNS, DHCP.                                                                 |

### **Architecture**
- **VLANs** pour isolation des départements :
  - VLAN 10 : Direction Générale.
  - VLAN 20 : Direction Marketing.
  - VLAN 30 : RH.
  - VLAN 40 : Commercial nomade.
  - VLAN 50 : Invités (Wi-Fi public séparé).
- **Plan d’adressage IP** (192.168.X.0/24 pour chaque VLAN).
- **Routeur central** pour gérer le routage inter-VLAN.

---

## **4. Convention de nommage**

- **Postes utilisateurs :** `PC-<Département>-<NomUtilisateur>`
  - Exemple : `PC-DSI-JDupont`.
- **Serveurs :** `SRV-<Fonction>`
  - Exemple : `SRV-AD`, `SRV-DHCP`.
- **Switches :** `SW-<Étage>`
  - Exemple : `SW-1`, `SW-2`.
- **Routeurs :** `RTR-<NomZone>`
  - Exemple : `RTR-MAIN`, `RTR-BACKUP`.

---

## **5. Table de routage**

| **Réseau/VLAN** | **Adresse réseau** | **Passerelle**      | **Masque**   | **Interface** |
|------------------|--------------------|---------------------|--------------|---------------|
| VLAN 10          | 192.168.10.0      | 192.168.10.1        | 255.255.255.0| LAN1          |
| VLAN 20          | 192.168.20.0      | 192.168.20.1        | 255.255.255.0| LAN2          |
| VLAN 30          | 192.168.30.0      | 192.168.30.1        | 255.255.255.0| LAN3          |

---

## **6. Suivi des objectifs du projet**

### **Template choisi :**

- **Onglet Objectifs :** Catégories principales, secondaires, optionnels.
- **Onglet Suivi individuel :** Attribution des tâches hebdomadaires.
- **Onglet PRA :** Préparation pour la continuité en cas de panne critique.

---

## **Conclusion**

Ce plan assure une transition structurée vers une infrastructure réseau sécurisée et scalable. La priorité est donnée à la sécurité, à la centralisation des données, et à la préparation à l’expansion future.

