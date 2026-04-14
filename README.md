# Analyse Forensique d'un iPhone
*Étude des artefacts numériques et de l'activité utilisateur*

---

## 📌 Sommaire
1. [Comptes Utilisateur](#1-comptes-utilisateur)
2. [Applications Installées](#2-applications-installées)
3. [Contacts Utilisateur](#3-contacts-utilisateur)
4. [Activité d'Appels](#4-activité-dappels)
5. [Communications SMS/iMessage](#5-communications-sms--imessage)
6. [Stockage des Données d'Applications](#6-stockage-des-données-dapplications)
7. [Appairage de l'iPhone](#7-appairage-de-liphone)
8. [Connexions Wi-Fi](#8-connexions-wi-fi)
9. [Analyse du Trafic Réseau](#9-analyse-du-trafic-réseau)

---

## 1. Comptes Utilisateur
### ❓ Quels sont les comptes utilisateurs présents ?
**Réponse** :
Le compte principal identifié est **thisisdfir@gmail.com**, associé aux services suivants :
- Compte Apple (iCloud)
- Compte Google (Gmail)
- Services Apple (localisation, synchronisation, etc.)

**Preuves** :
- **Fichier** : `/private/var/mobile/Library/Accounts/Accounts3.sqlite`
- **Champs** :
  - `ZUSERNAME = thisisdfir@gmail.com`
  - `ZOWNINGBUNDLEID = com.apple.AuthKit`
  - Services : `com.apple.accountsd`, `com.apple.purplebuddy`

---

## 2. Applications Installées
### ❓ Quelles sont les applications installées ?
**Liste des applications** :
- **Messagerie** : WhatsApp, Signal, Telegram, Discord, Slack, LINE, Kik, Viber
- **Réseaux sociaux** : Instagram, Twitter, Reddit, TikTok
- **Autres** : Spotify, Firefox Focus, OnionBrowser, Venmo

**Preuves** :
- **Répertoire** : `/private/var/containers/Bundle/Application/`
- **Justification** : Les fichiers `.app` présents correspondent aux applications installées.

---

## 3. Contacts Utilisateur
### ❓ Combien de contacts l'utilisateur possède-t-il ?
**Réponse** :
- **3 enregistrements** de contacts ont été identifiés, mais seulement **2 contacts uniques** après corrélation.

**Détails** :
- **Contact A** :
  - Email : thisisdfirtwo@gmail.com
  - Téléphone : (919) 888-7386
- **Contact B** : Doublon du Contact A
- **Contact C** :
  - Email : joshuahickman957@gmail.com
  - Téléphones : (919) 579-0479, (919) 391-2507

**Preuves** :
- **Fichier** : `/private/var/mobile/Library/AddressBook/`

---

## 4. Activité d'Appels
### ❓ Analyse des communications téléphoniques
**Réponse** :
- L'utilisateur a effectué des appels **entrants/sortants**, **répondus/manqués**, et utilisé **FaceTime**.

**Preuves** :
- **Fichier** : `/private/var/mobile/Library/CallHistoryDB/CallHistory.storedata`
- **Champs** :
  - `ZDATE` : Horodatage
  - `ZDURATION` : Durée
  - `ZORIGINATED` : Type d'appel (entrant/sortant)
  - `ZCALLTYPE` : Type (téléphonie/FaceTime)

---

## 5. Communications SMS/iMessage
### ❓ Analyse des conversations
**Conversations identifiées** :
1. **Conversation 1** :
   - Participants : `personne_1`, `personne_2`
   - Messages échangés sur la synchronisation entre Mac et iPhone, et l'envoi de photos.

2. **Conversation 2** :
   - Participants : `personne_1`, `personne_2`
   - Messages sur des problèmes techniques.

**Preuves** :
- **Fichier** : `/private/var/mobile/Library/SMS/sms.db`

---

## 6. Stockage des Données d'Applications
### ❓ Comment sont stockées les données des applications ?
**Formats identifiés** :
- **Bases de données** : `.sqlite`, `.db` (ex: `ChatStorage.sqlite` pour WhatsApp)
- **Fichiers PLIST** : `.plist` (ex: `StatusMessages.plist`, `SyncHistory.plist`)
- **Logs** : `.log` (ex: `whatsapp-2021-02-15...launch.log`)
- **Fichiers binaires** : `.dat`, `.cache` (ex: `fsCachedData`)
- **Multimédias** : `.jpg`, `.png`, `.mp4`

**Emplacements** :
- `Library/Application Support/`
- `Documents/`
- `Library/Preferences/`
- `Library/Logs/`
- `Library/Caches/`

---

## 7. Appairage de l'iPhone
### ❓ L'iPhone a-t-il été appairé ?
**Réponse** :
Oui, avec **au moins un appareil** (un ordinateur nommé "Joshua’s Mac mini").

**Preuves** :
- **Dossier** : `/private/var/root/Library/Lockdown/pair_records/`
- **Fichiers** :
  - Certificats d'appairage (`HostCertificate`, `RootCertificate`)
  - `data_ark.plist` : Contient `com.apple.itunes.backup-LastBackupComputerName = Joshua’s Mac mini`

---

## 8. Connexions Wi-Fi
### ❓ L'iPhone s'est-il connecté à des réseaux Wi-Fi ?
**Réponse** :
Oui, le fichier `com.apple.wifi.plist` confirme l'utilisation de réseaux Wi-Fi.

**Preuves** :
- **Fichier** : `/private/var/preferences/SystemConfiguration/com.apple.wifi.plist`
- **Contenu** : Liste des réseaux Wi-Fi connus (`KnownNetworks`).

---

## 9. Analyse du Trafic Réseau
### ❓ Quel processus a transmis/reçu le plus de données ?
**Wi-Fi** :
- **Réception max** : `parsecd` (Z_PK 90)
- **Transmission max** : `mediaserverd` (Z_PK 91)

**WAN (Cellulaire)** :
- **Réception max** : `com.apple.appstored` (Z_PK 122)
- **Transmission max** : `terminusd/com.apple.mobileassetd` (Z_PK 116)

---

## 📊 Synthèse
   Catégorie                | Détails                                                                                     |
 |--------------------------|---------------------------------------------------------------------------------------------|
 | **Comptes utilisateur**   | `thisisdfir@gmail.com` (iCloud, Gmail)                                                      |
 | **Applications**          | WhatsApp, Signal, Telegram, Instagram, Spotify, etc.                                         |
 | **Contacts**             | 2 contacts uniques                                                                          |
 | **Appels**               | Appels entrants/sortants, FaceTime                                                           |
 | **SMS/iMessage**         | Conversations avec `personne_1` et `personne_2`                                             |
 | **Stockage des données**  | Bases de données, PLIST, logs, fichiers binaires, multimédias                                |
 | **Appairage**            | Oui, avec "Joshua’s Mac mini"                                                                |
 | **Wi-Fi**                | Oui, réseaux enregistrés dans `com.apple.wifi.plist`                                        |
 | **Trafic réseau**        | `parsecd` (réception Wi-Fi), `mediaserverd` (transmission Wi-Fi), `com.apple.appstored` (WAN) |

---
