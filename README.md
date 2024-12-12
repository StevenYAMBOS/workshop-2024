# Guide d'utilisation

<p align="center">
  <a href="https://youtu.be/3FmN46XQius" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2022/10/ESP32-Getting-Started.jpg?resize=1024%2C576&quality=100&strip=all&ssl=1" width="800" alt="ESP32 guide" /></a>
</p>

---

## Sommaire

- [Introduction](#introduction)
- [I - Technologies utilisées](#i---technologies-utilisées)
  - [Matériel](#matériel)
  - [Logiciel](#logiciel)
- [II - Manuel d'utilisation](#ii---manuel-dutilisation)
  - [Accès à l'application](#accès-à-lapplication)
  - [Tableau de bord](#tableau-de-bord)
  - [Graphiques](#graphiques)
  - [Notifications](#notifications)
    - [Code couleur des indicateurs](#code-couleur-des-indicateurs)
    - [Seuils de qualité de l'air](#seuils-de-qualité-de-lair)
    - [Interprétation des alertes](#interprétation-des-alertes)
    - [Rappel des normes](#rappel-des-normes)
    - [Exemples de notifications](#exemples-de-notifications)
- [III - Instructions d’installation](#iii---instructions-dinstallation)
  - [Préparation du matériel](#préparation-du-matériel)
    - [Composants requis](#composants-requis)
    - [Schéma de câblage](#schéma-de-câblage)
  - [Configuration de Firebase](#configuration-de-firebase)
    - [Créer un projet Firebase](#créer-un-projet-firebase)
    - [Configurez Real Time Database](#configurez-real-time-database)
    - [Configurez Authentication](#configurez-authentication)
  - [Programmation de l’ESP32](#programmation-de-lesp32)
    - [Installer Arduino IDE](#installer-arduino-ide)
    - [Installer les bibliothèques nécessaires](#installer-les-bibliothèques-nécessaires)
    - [Configurer le code Arduino](#configurer-le-code-arduino)
  - [Tests du système](#tests-du-système)
    - [Vérifier les connexions](#vérifier-les-connexions)
    - [Vérifier les données dans Firebase](#vérifier-les-données-dans-firebase)
  - [Développement de l’interface utilisateur](#développement-de-linterface-utilisateur)
    - [Configurez un projet Next.js](#configurez-un-projet-nextjs)
    - [Créez une page de tableau de bord](#créez-une-page-de-tableau-de-bord)
    - [Déployez l’interface sur Vercel](#déployez-linterface-sur-vercel)
  - [Déploiement réel](#déploiement-réel)
- [Glossaire des termes](#glossaire-des-termes)
- [Développeurs](#développeurs)

---

## Introduction

Ce système fournit une solution complète pour surveiller les conditions environnementales d'un espace en temps réel. Les données sont accessibles depuis une interface utilisateur web intuitive. Ce guide a pour objectif de vous accompagner dans la compréhension de son fonctionnement. Pour toute assistance, contactez les développeurs du projet.

---

## I - Technologies utilisées

### Matériel

- ![Espressif](https://img.shields.io/badge/espressif-E7352C.svg?style=for-the-badge&logo=espressif&logoColor=white) **(ESP32-WROOM-32E)** : Microcontrôleur qui collecte et transmet les données des capteurs à Firebase.
- **Capteur SCD30** : Mesure les niveaux de CO2, la température et l'humidité.
- **Batterie (LiPo 3.7V 1800mAh)** : Fournit une alimentation mobile à l'ESP32 pour les tests réels.

### Logiciel

-     ![Arduino](https://img.shields.io/badge/-Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white) : IDE utilisé pour programmer l'ESP32.
- ![Firebase](https://img.shields.io/badge/firebase-a08021?style=for-the-badge&logo=firebase&logoColor=ffcd34) : Stocke les données collectées par le capteur et les rend accessibles en temps réel.
- <img src="https://imgs.search.brave.com/McPVWjrj_VznjvWVtdprpS1RisZF6EtpOwBr6_MmERc/rs:fit:860:0:0:0/g:ce/aHR0cHM6Ly9zZWVr/bG9nby5jb20vaW1h/Z2VzL0EvYXV0b2Rl/c2stZnVzaW9uLTM2/MC1sb2dvLTdGNzJB/NzYzOTctc2Vla2xv/Z28uY29tLnBuZw" width="40px" alt="Autodesk Fusion logo" /> : Utilisé pour concevoir la modélisation 3D du dispositif.
- ![Next JS](https://img.shields.io/badge/Next-black?style=for-the-badge&logo=next.js&logoColor=white) : Framework pour créer une interface utilisateur moderne.
- ![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=for-the-badge&logo=tailwind-css&logoColor=white) : Framework CSS pour le style rapide et efficace de l'interface.
- ![Vercel](https://img.shields.io/badge/vercel-%23000000.svg?style=for-the-badge&logo=vercel&logoColor=white) : Plateforme de déploiement pour héberger l'interface utilisateur.
- ![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white) : Système d'exploitation utilisé pour le développement et la configuration.

---

## II - Manuel d'utilisation

### Accès à l'application

L'application est accessible à partir de ce lien : [https://workshop2024](https://workshop2024).

### Tableau de bord

La page d'accueil affiche les données environnementales collectées par le capteur sous forme de widgets interactifs. Ces données sont centralisées en temps réel depuis Firebase et organisées en trois sections principales :

- Niveau de `CO2`
- Niveau de `température`
- Niveau d'`humidité`

Les valeurs affichées reflètent l'état le plus récent de l'espace surveillé.

### Graphiques

Les données collectées sont également présentées sous forme de graphiques dynamiques. Ces graphiques permettent de visualiser l'évolution des paramètres environnementaux sur différentes périodes, telles que :

- Heures
- Jours
- Semaines
- Mois

Cela permet aux utilisateurs de mieux comprendre les tendances environnementales et de prendre des décisions éclairées.

### Notifications

Les notifications visuelles sont conçues pour alerter les utilisateurs des variations environnementales dans leur espace en fonction des [seuils de qualité de l'air définis](https://www.airparif.fr/la-reglementation-en-france). Les indicateurs suivent un code couleur pour refléter l'état actuel de l'environnement.

#### Code couleur des indicateurs

- **Vert** : Valeurs normales — environnement sain.
- **Orange** : Valeurs proches des seuils critiques — attention recommandée.
- **Rouge** : Valeurs dangereuses — intervention immédiate requise.

#### Seuils de qualité de l'air

Les seuils ci-dessous sont définis pour les paramètres mesurés par le capteur et visent à aligner les alertes sur les [normes en vigueur](https://www.airparif.fr/la-reglementation-en-france).

| **Paramètre**        | **Vert (Normal)** | **Orange (Attention)** | **Rouge (Danger)** |
| -------------------- | ----------------- | ---------------------- | ------------------ |
| **CO2 (ppm)**        | ≤ 800             | 801 - 1200             | > 1200             |
| **Température (°C)** | 20 - 26           | 18 - 19 ou 27 - 30     | < 18 ou > 30       |
| **Humidité (%)**     | 40% - 60%         | 30% - 39% ou 61% - 70% | < 30% ou > 70%     |

---

#### Interprétation des alertes

- **Rouge** :

  - CO2 > 1200 ppm : Risque élevé pour la santé. Aérez immédiatement l’espace.
  - Température < 18 °C ou > 30 °C : Conditions inconfortables pouvant affecter la santé ou la productivité.
  - Humidité < 30% ou > 70% : Risques pour la santé respiratoire et les équipements électroniques.

- **Orange** :

  - CO2 entre 801 - 1200 ppm : Concentrez-vous sur l’aération de la pièce.
  - Température entre 18-19 °C ou 27-30 °C : Environnement légèrement inconfortable. Surveillez l’évolution.
  - Humidité entre 30-39% ou 61-70% : Conditions sous-optimales. Prenez des mesures si nécessaire.

- **Vert** :
  - CO2 ≤ 800 ppm, température entre 20-26 °C et humidité entre 40-60% : L’espace est dans des conditions optimales.

---

#### Rappel des normes

- **CO2** :
  - Une concentration de CO2 supérieure à 1000 ppm peut causer des troubles de concentration.
  - Au-delà de 1200 ppm, des effets plus sérieux sur la santé peuvent apparaître (fatigue, maux de tête).
- **Température** :
  - L'intervalle optimal pour les espaces de travail est entre 20 et 26 °C.
  - Une température inadéquate peut entraîner de l'inconfort et des problèmes de santé.
- **Humidité** :
  - L'humidité relative idéale pour les espaces fermés est de 40 à 60 %.
  - Une humidité trop basse favorise les infections respiratoires, tandis qu'une humidité élevée peut provoquer de la moisissure.

---

#### Exemples de notifications

1. **CO2 : 1300 ppm**  
   _Alerte Rouge — Danger_  
   **Message** : "Niveau critique de CO2 détecté. Aérez immédiatement la pièce pour réduire la concentration."

2. **Température : 28 °C**  
   _Alerte Orange — Attention_  
   **Message** : "Température élevée détectée. Envisagez une ventilation ou une climatisation pour améliorer le confort."

3. **Humidité : 65 %**  
   _Alerte Orange — Attention_  
   **Message** : "Niveau d'humidité élevé. Vérifiez la ventilation ou utilisez un déshumidificateur."

---

### Glossaire des termes

Glossaire de l'application :

**ESP32**

Un microcontrôleur puissant conçu pour les projets IoT (Internet des Objets). Il intègre Wi-Fi et Bluetooth, ce qui le rend idéal pour des applications connectées en temps réel.

**SCD30**

Un capteur avancé capable de mesurer :

- **CO2 (Dioxyde de Carbone)** : Mesure les niveaux de dioxyde de carbone dans l'air (en ppm).
- **Température** : Mesure la température ambiante (en °C).
- **Humidité relative** : Mesure l'humidité dans l'air (en %).

**Firebase Real Time Database**

Une base de données cloud fournie par Google qui permet de stocker et de synchroniser les données en temps réel entre plusieurs clients.

**Arduino IDE**

Un environnement de développement intégré (IDE) utilisé pour programmer des microcontrôleurs comme l'ESP32. Il fournit une interface simple pour écrire et téléverser des scripts.

**NTP (Network Time Protocol)**

Un protocole utilisé pour synchroniser l'heure de l'ESP32 avec un serveur distant. Cela permet de récupérer un horodatage précis.

**NextJS**

Un framework JavaScript basé sur React.js, utilisé pour développer des applications web modernes. Il facilite la création d'applications performantes avec rendu côté serveur et génération statique.

**Tailwind CSS**

Un framework CSS utilitaire qui simplifie le processus de stylisation des interfaces utilisateur en utilisant des classes pré-définies.

**Vercel**

Une plateforme de déploiement qui héberge des applications web. Elle est utilisée ici pour déployer l'interface utilisateur Next.js.

**ChartJS**

Une bibliothèque JavaScript pour créer des graphiques interactifs et visuels dans les applications web. Elle est utilisée pour représenter les données collectées sous forme graphique.

**PWA (Progressive Web App)**

Une application web optimisée pour offrir une expérience utilisateur similaire à une application native, y compris le mode hors-ligne et la possibilité d'être installée sur un appareil mobile.

---

## III - Instructions d’installation

Cette section détaille les étapes nécessaires pour configurer, tester et déployer le système de surveillance environnementale basé sur l’ESP32, le capteur SCD30, et Firebase.

---

### Préparation du matériel

#### Composants requis

- **ESP32-WROOM-32E** : Microcontrôleur pour collecter et envoyer les données.
- **Capteur SCD30** : Mesure les niveaux de CO2, la température et l'humidité.
- **Batterie LiPo (3.7V 1800mAh)** : Fournit une alimentation mobile à l'ESP32 pour les tests réels.
- **Câbles Dupont** : Pour connecter le capteur à l'ESP32.
- **Câble USB Type-C/Micro-USB** : Pour connecter l'ESP32 à un PC.

#### Schéma de câblage

1. **Connectez les broches du capteur SCD30 à l'ESP32** :

   - **SDA** du capteur → GPIO21 (SDA) de l’ESP32.
   - **SCL** du capteur → GPIO22 (SCL) de l’ESP32.
   - **VCC** du capteur → 3.3V ou VCC de l’ESP32.
   - **GND** du capteur → GND de l’ESP32.

<p align="center">
  <a href="https://www.youtube.com/watch?v=MicAM_A0_lU" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2022/10/ESP32-labelled.jpg?w=750&quality=100&strip=all&ssl=1" width="400" alt="ESP32 branchements" /></a>
</p>

2. **Branchez l’ESP32** :
   - Connectez l’ESP32 à votre PC via un câble USB pour les tests.
   - Pour les tests réels, connectez une batterie LiPo compatible.

---

### Configuration de Firebase

#### Créer un projet Firebase

1. Connectez-vous à [Firebase Console](https://console.firebase.google.com/).
2. Cliquez sur **Créer un projet** et suivez les instructions.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/1-Set-Up-Firebase-Project-ESP32-ESP8266.png?w=680&quality=100&strip=all&ssl=1" width="400" alt="ESP32 branchements" /></a>
</p>

3. Une fois le projet créé, accédez à la section **Paramètres du projet** et copiez les informations suivantes :
   - **Clé API Web**.
   - **URL de la base de données**.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/1-Get-Firebase-Project-API-Key.png?w=750&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Firebase" /></a>
</p>

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/2-Get-Firebase-Project-API-Key.png?w=792&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Firebase" /></a>
</p>

#### Configurez Real Time Database

1. Dans Firebase Console, accédez à **Créer > Real Time Database**.
2. Cliquez sur **Créer une base de données**.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/1-Set-Up-Firebase-database-ESP32-ESP8266.png?w=750&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Firebase" /></a>
</p>

3. Sélectionnez le mode **Test** pour permettre des lectures et écritures temporaires.
4. Ajoutez les règles suivantes pour les tests :
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/3-Set-Up-Firebase-database-ESP32-ESP8266.png?w=776&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Firebase" /></a>
</p>

#### Configurez Authentication

1. Accédez à **Créer > Authentication**.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/5-Set-Up-Firebase-Project-ESP32-ESP8266.png?w=750&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Firebase" /></a>
</p>

2. Activez l’authentification par **`Anonyme`**.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/6-Set-Up-Firebase-Project-ESP32-ESP8266.png?w=750&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Firebase" /></a>
</p>

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/08/7-Set-Up-Firebase-Project-ESP32-ESP8266.png?w=842&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Firebase" /></a>
</p>

---

### Programmation de l’ESP32

#### Installer Arduino IDE

1. Téléchargez et installez [Arduino IDE](https://www.arduino.cc/en/Main/Software). Nous vous conseillons de travailler sur le système d'exploitation **Windows** ou **MacOS**.**Linux** ne dispose pas des pilotes nécessaires pour l'ESP32 :

- **Windows** : exécutez le fichier téléchargé et suivez les instructions du guide d'installation.
- **MacOS X** : copier le fichier téléchargé dans votre dossier d'application.
- **Linux** : extraire le fichier téléchargé, et ouvrir le fichier arduino-ide qui lancera l'IDE.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2022/11/download-arduino-ide-2-3-2.png?w=865&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Arduino" /></a>
</p>

2. Ajoutez le gestionnaire de cartes ESP32 :
   - Accédez à **Fichier > Préférences**.
   - Dans le champ **URL supplémentaire pour les gestionnaires de cartes**, ajoutez :

     ```shell
     https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
     ```

   - Allez dans **Outils > Gestionnaire de cartes**, recherchez "ESP32" et installez le package.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/05/Arduino-IDE-2-preferences-additional-boards-manager-esp32.png?w=797&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Arduino" /></a>
</p>

#### Installer les bibliothèques nécessaires

1. Ouvrez **Outils > Gérer les bibliothèques** et installez :
   - **Firebase Arduino Client Library for ESP8266 & ESP32**
   - **Adafruit SCD30**
   - **RTCLib**
   - **NTPClient** (facultatif)

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/05/arduino-ide-2-boards-manager.png?w=799&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Arduino" /></a>
</p>

#### Configurer le code Arduino

1. Ouvrez un nouveau projet dans Arduino IDE.
2. Ajoutez le code corrigé fourni précédemment.
3. Modifiez les variables suivantes dans le code :

   - **WIFI_SSID** : Nom de votre réseau Wi-Fi.
   - **WIFI_PASSWORD** : Mot de passe de votre réseau Wi-Fi.
   - **API_KEY** : Clé API Firebase.
   - **DATABASE_URL** : URL de votre base de données Firebase.

4. Téléversez le code sur l’ESP32 :
   - Sélectionnez le bon port série sous **Outils > Port**.
   - Cliquez sur **Téléverser**.

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2024/02/arduino-ide-2-select-board.png?w=750&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Arduino" /></a>
</p>

<p align="center">
  <a href="https://firebase.google.com/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2021/05/arduino-ide-2-select-board-esp32.png?w=622&quality=100&strip=all&ssl=1" width="400" alt="Paramètres Arduino" /></a>
</p>

⚠️ Installer ce pilote si le port n'apparaît pas, suivre ce tuto : https://randomnerdtutorials.com/install-esp32-esp8266-usb-drivers-cp210x-windows/⚠️

---

### Tests du système

#### Vérifier les connexions

1. Ouvrez le **Moniteur Série** dans Arduino IDE pour afficher les logs.
2. Vérifiez que :
   - L’ESP32 se connecte au Wi-Fi.
   - Les données du capteur SCD30 sont collectées.
   - Les données sont envoyées à Firebase.

#### Vérifier les données dans Firebase

1. Accédez à votre base de données dans Firebase Console.
2. Assurez-vous que les données sont stockées avec la structure suivante :

   ```json
   dc_Campus
      └── 3.2
          └── <id unique>
              └── co2
              └── temperature
              └── humidity
              └── battery_voltage
              └── date (timestamp UNIX)
   ```

---

### Développement de l’interface utilisateur

#### Configurez un projet Next.js

1. Créez une application Next.js en exécutant :
   ```bash
   npx create-next-app@latest
   ```
2. Installez Firebase SDK pour interagir avec la base de données :
   ```bash
   npm install firebase
   # ou
   yarn install firebase
   ```

#### Créez une page de tableau de bord

1. Ajoutez une connexion à Firebase pour récupérer les données en temps réel.
2. Utilisez des graphiques interactifs (par exemple, avec **Chart.js**) pour afficher les données collectées.

#### Déployez l’interface sur Vercel

1. Connectez votre projet Next.js à [Vercel](https://vercel.com/).
2. Déployez l’application et obtenez une URL accessible au public.

---

### Déploiement réel

1. Installez le système dans un environnement réel (par exemple, une salle ou un bureau).
2. Connectez l’ESP32 à une batterie pour le rendre mobile.
3. Surveillez les données en temps réel via l’interface utilisateur.

---

### Développeurs

- [Allan GARNIER](https://github.com/AlanGarnier)
- [Zohra HUSSAIN](https://github.com/Zoh-ra)
- [Samuel NDJOULI](https://github.com/samuelndjouli997)
- [Steven YAMBOS](https://github.com/StevenYAMBOS)
