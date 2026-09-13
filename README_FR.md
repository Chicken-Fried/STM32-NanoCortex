# ⚡ NanoCortex-F042 : Carte de Développement ARM Cortex-M0 Minimaliste

[![KiCad](https://img.shields.io/badge/KiCad-8.0-blue.svg?logo=kicad)](https://www.kicad.org/)
[![Hardware](https://img.shields.io/badge/Open%20Source-Hardware-green.svg)](https://freedomdefined.org/OSHW)
[![MCU](https://img.shields.io/badge/MCU-STM32F042-orange.svg?logo=stmicroelectronics)](https://www.st.com/)
[![License: MIT](https://img.shields.io/badge/Licence-MIT-yellow.svg)](LICENSE)

Une carte de développement 32 bits autonome et pratique (**26 mm × 36 mm**), inspirée par l'esprit et la simplicité minimaliste des cartes Arduino ATtiny, mais optimisée pour le prototypage sur table (*devboard*). Elle est propulsée par le microcontrôleur **STM32F042** (ARM Cortex-M0) avec USB-C natif sans quartz.

[Read English Version](README.md)

---

## 🌟 Pourquoi ce projet ?

Ce projet est né au croisement de mes études en électronique, de ma curiosité et de la passion du prototypage *DIY* :

1. **Relier la théorie et la pratique :** Mettre en application concrète les enseignements de mes cours d'électronique (saisie de schéma, sélection rigoureuse des composants, intégrité des signaux, règles de routage PCB sous KiCad).
2. **Plonger dans l'univers 32 bits :** Dépasser les limites des architectures 8 bits classiques (AVR, ATtiny) pour monter en compétences sur l'écosystème moderne des microcontrôleurs ARM Cortex.
3. **Le plaisir d'apprendre (*For fun*) :** Un passe-temps enrichissant et complémentaire à mon cursus pour expérimenter la gestion de l'USB matériel, la faible consommation et la programmation bas-niveau.
4. **Partager en Open Source :** Offrir une base matérielle propre, minimaliste et bien documentée pour les étudiants, makers et curieux.
5. **Valider la faisabilité sur le terrain :** Tester et éprouver cette carte tout au long de l'année scolaire sur des cas d'usages réels (pilotage de relais, interface graphique sur écran OLED, fonctionnement sur pile) pour confronter la théorie à la réalité physique.

---

## ✨ Points Forts de la Carte

* **🧠 Cœur de calcul :** STMicroelectronics **STM32F042F6P6** (ARM Cortex-M0 cadencé à 48 MHz, 32 Ko Flash, 6 Ko RAM).
* **🔌 USB-C sans quartz (*Crystal-less*) :** Utilisation de l'oscillateur interne 48 MHz (`HSI48`) couplé au système de récupération d'horloge (`CRS`) synchronisé directement sur le bus USB. **Aucun composant ni quartz externe n'est requis.**
* **🚀 Téléversement direct sans programmateur (DFU natif) :** Bootloader USB officiel gravé en mémoire morte (ROM). En maintenant le bouton `BOOT` à la mise sous tension, la carte est immédiatement reconnue par l'ordinateur et prête à être flashée via `STM32CubeProgrammer` ou `dfu-util` (pas besoin de sonde ST-Link obligatoire).
* **📐 Format Devboard Pratique (26 mm × 36 mm) :** Dimensions pensées pour un usage confortable sur établi de laboratoire, avec des connecteurs aérés, faciles d'accès pour les câbles Dupont et les pointes de test d'oscilloscope.
* **⚡ Alimentation 3.3V stabilisée :** Régulateur LDO intégré à faible chute de tension et découplage capacitif soigné pour garantir une tension 3.3V propre.
* **🎛️ Boutons tactiles intégrés :** Deux micro-boutons-poussoirs en face avant pour le `RESET` et le mode `BOOT0`.
* **🛠️ Conçu pour la fabrication moderne :** Règles de routage 2 couches optimisées pour une fabrication économique chez les fabricants de circuits imprimés (ex: JLCPCB).

---

## 📋 Fiche Technique

| Caractéristique | Spécification |
| :--- | :--- |
| **Microcontrôleur** | STM32F042F6P6 (boîtier TSSOP-20) |
| **Architecture** | ARM 32-bit Cortex-M0 (jusqu'à 48 MHz) |
| **Mémoire** | 32 Ko Flash / 6 Ko SRAM |
| **Tension de fonctionnement** | 3.3V logique (Entrée : 5V via USB-C ou broche 3.3V directe) |
| **Interface USB** | USB 2.0 Full Speed (12 Mbps) sur connecteur USB-C |
| **Entrées / Sorties (GPIO)** | Jusqu'à 14 broches accessibles (I2C, SPI, USART, PWM, ADC) |
| **Modes de programmation** | USB DFU natif en ROM + pastilles de test SWD |
| **Dimensions** | **26 mm × 36 mm** |

---

## 🛠️ Conception Électronique & Routage

### Alimentation & Protection
* **Connecteur USB-C :** Intégration de deux résistances de rappel à la masse de 5,1 kΩ sur les broches `CC1` et `CC2`, assurant la reconnaissance par tous les chargeurs et câbles USB-C vers USB-C modernes.
* **Régulateur LDO :** Conversion propre du 5V USB vers le 3.3V pour alimenter le microcontrôleur et les périphériques.
* **Filtrage et découplage :** Condensateurs céramiques multi-étages placés au plus près des broches $V_{DD}$ et $V_{DDA}$.

### Routage USB
* **Paire différentielle :** Pistes $D^+$ et $D^-$ routées parallèlement en face supérieure avec plan de masse continu ininterrompu en face inférieure pour garantir l'intégrité du signal haute fréquence sans réflexions parasites.

---

## 💻 Mise en Route & Programmation

### 1. Passer en mode Bootloader USB (DFU)
Aucun programmateur externe n'est nécessaire :
1. Maintenez enfoncé le bouton **BOOT**.
2. Appuyez puis relâchez le bouton **RESET** (ou branchez le câble USB-C).
3. Relâchez le bouton **BOOT**.
4. Votre système d'exploitation détecte la puce comme **STM32 BOOTLOADER**.

### 2. Flasher le binaire
Vous pouvez téléverser votre code compilé (`.bin` ou `.hex`) avec :
* L'utilitaire graphique officiel **STM32CubeProgrammer**.
* Ou en ligne de commande via **dfu-util** :
  ```bash
  dfu-util -a 0 -d 0483:df11 --dfuse-address 0x08000000 -D mon_firmware.bin
  ```

### 3. Environnements de développement supportés
* **STM32CubeIDE :** En C/C++ natif avec les bibliothèques STM32 HAL ou LL (Low-Layer).
* **Arduino IDE / PlatformIO :** Prise en charge complète via le core officiel [STM32duino](https://github.com/stm32duino/Arduino_Core_STM32).

---

## 🎯 Feuille de Route & Expérimentations de l'Année

Ce dépôt documente l'évolution et les tests pratiques de la carte tout au long de l'année :
- [x] Schématique électrique sous KiCad 8.
- [x] Routage 2 couches avec paire différentielle USB optimisée.
- [ ] Commande des prototypes et assemblage des composants CMS.
- [ ] Test et validation du téléversement via USB DFU natif.
- [ ] **Expérience 1 :** Création d'une interface graphique avec menu interactif sur écran OLED 0.96" I2C (SSD1306) via la librairie U8g2.
- [ ] **Expérience 2 :** Commande de charges inductives et pilotage de 2 relais avec transistors de commutation et diodes de roue libre.
- [ ] **Expérience 3 :** Étude de la consommation et fonctionnement autonome sur batterie 3.3V (LiFePO4 ou Li-Ion).

---

## 🤝 Partage & Contributions

Les retours, conseils et améliorations sont les bienvenus ! Que vous soyez étudiant, passionné ou ingénieur expérimenté, n'hésitez pas à ouvrir une **Issue** pour poser une question ou à soumettre une **Pull Request**.

---

## 📜 Licence

Ce projet est distribué sous licence [MIT](LICENSE). Vous êtes libre de l'utiliser, le reproduire et l'adapter pour vos propres projets et apprentissages !
