# Guide d'utilisation

<p align="center">
  <a href="https://randomnerdtutorials.com/getting-started-with-esp32/" target="blank"><img src="https://i0.wp.com/randomnerdtutorials.com/wp-content/uploads/2022/10/ESP32-Getting-Started.jpg?resize=1024%2C576&quality=100&strip=all&ssl=1" width="800" alt="ESP32 guide" /></a>
</p>

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
- [Développeurs](#développeurs)

## Introduction

Ce système fournit une solution complète pour surveiller les conditions environnementales d'un espace en temps réel. Les données sont accessibles depuis une interface utilisateur web intuitive. Ce guide a pour objectif de vous accompagner dans la compréhension de son fonctionnement. Pour toute assistance, contactez les développeurs du projet.

---

## I - Technologies utilisées

### Matériel

- ![Espressif](https://img.shields.io/badge/espressif-E7352C.svg?style=for-the-badge&logo=espressif&logoColor=white) **(ESP32-WROOM-32E)** : Microcontrôleur qui collecte et transmet les données des capteurs à Firebase.
- **Capteur SCD30** : Mesure les niveaux de CO2, la température et l'humidité.
- **Batterie (LiPo 3.7V 1800mAh)** : Fournit une alimentation mobile à l'ESP32 pour les tests réels.

### Logiciel

- 	![Arduino](https://img.shields.io/badge/-Arduino-00979D?style=for-the-badge&logo=Arduino&logoColor=white) : IDE utilisé pour programmer l'ESP32.
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

| **Paramètre**   | **Vert (Normal)**                    | **Orange (Attention)**                | **Rouge (Danger)**                          |
|------------------|--------------------------------------|----------------------------------------|---------------------------------------------|
| **CO2 (ppm)**    | ≤ 800                               | 801 - 1200                             | > 1200                                      |
| **Température (°C)** | 20 - 26                           | 18 - 19 ou 27 - 30                     | < 18 ou > 30                                |
| **Humidité (%)** | 40% - 60%                           | 30% - 39% ou 61% - 70%                 | < 30% ou > 70%                              |

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

Cette configuration garantit que votre système alerte efficacement les utilisateurs tout en respectant les réglementations et normes de qualité de l'air. Vous pouvez personnaliser davantage les messages ou les seuils en fonction des spécificités de votre application.

## Développeurs

- [Allan GARNIER](https://github.com/AlanGarnier)
- [Zohra HUSSAIN](https://github.com/Zoh-ra)
- [Samuel NDJOULI](https://github.com/samuelndjouli997)
- [Steven YAMBOS](https://github.com/StevenYAMBOS)
