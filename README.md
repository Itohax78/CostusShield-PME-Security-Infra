# 🛡️ CostusShield - Infrastructure de Sécurité Open Source pour PME

![pfSense](https://img.shields.io/badge/pfSense-2.7-red?style=flat-square&logo=pfsense)
![IPSec](https://img.shields.io/badge/VPN-IPSec%20%7C%20OpenVPN-blue?style=flat-square)
![Suricata](https://img.shields.io/badge/IDS%2FIPS-Suricata-orange?style=flat-square)

## 📋 Contexte du Projet
Ce projet a été réalisé dans le cadre du **Mastercamp Cybersécurité (EFREI Paris)**. L'objectif était de concevoir, déployer et documenter une architecture réseau hautement sécurisée pour une PME, en remplaçant les licences propriétaires coûteuses par une infrastructure 100% Open Source. Le projet a été géré selon une approche hybride (Cycle en V / Méthodes Agiles).

## 🏗️ Architecture Technique et Réalisations

L'infrastructure a été déployée dans un environnement virtualisé (VMware) simulant deux sites géographiques distincts interconnectés via un réseau WAN simulé.

### 1. Pare-feu et Segmentation (pfSense)
* Déploiement d'un routeur/pare-feu pfSense.
* Sécurisation des accès d'administration (bannissement du HTTP au profit du HTTPS).
* Configuration des règles de filtrage strictes entre les zones WAN, LAN et DMZ.

### 2. Interconnexion Site-à-Site (VPN IPSec)
* Mise en place d'un tunnel **IPSec** entre le Site A (Siège) et le Site B (Succursale).
* **Cryptographie robuste (Recommandations ANSSI) :** Chiffrement `AES-256`, hachage `SHA-256`, échange de clés `Diffie-Hellman Group 14 (2048 bits)`.

### 3. Télétravail Sécurisé (OpenVPN & PKI)
* Création d'une **Infrastructure à Clés Publiques (PKI)** interne avec autorité de certification racine (RSA 4096 bits).
* Déploiement d'un serveur **OpenVPN** (Roadwarrior) avec génération de certificats individuels exportables (`.ovpn`) pour les télétravailleurs.

### 4. Détection d'Intrusions (IDS Suricata)
* Intégration du module **Suricata** sur les interfaces réseaux.
* Activation du jeu de règles *Emerging Threats (ETOpen)*.
* Détection validée via des simulations d'attaques agressives (`nmap -A`) sur le réseau.

### 5. Qualité de Service (QoS) & Résilience
* Déploiement du **Traffic Shaping (algorithme HFSC)** pour prioriser les flux critiques (VoIP, paquets ACK) et limiter la bande passante allouée aux flux de divertissement.
* **Automatisation / PRA :** Sauvegarde complète de la topologie réseau, des clés et des règles sous forme de fichier XML pour permettre une restauration (Plan de Reprise d'Activité) en moins de 2 minutes.

---

## 📁 Contenu de ce dépôt

Ce dépôt sert de portfolio technique et documentaire. Vous y trouverez :

* `📁 docs/` : L'intégralité des rapports techniques, d'architecture et de gestion de projet (WBS, RACI, Cycle en V).
* `📁 config_files/` : 
  * Le fichier `XML` de sauvegarde intégrale du pare-feu pfSense.
  * Le template de configuration client `OpenVPN (.ovpn)` pour les accès distants.

> **Note :** *Pour des raisons de sécurité, les fichiers de configuration présents dans ce dépôt sont issus d'un laboratoire de simulation isolé et ne contiennent pas de clés cryptographiques de production d'une véritable entreprise.*
