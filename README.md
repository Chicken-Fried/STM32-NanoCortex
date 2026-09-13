# ⚡ NanoCortex-F042: Minimalist ARM Cortex-M0 Development Board

[![KiCad](https://img.shields.io/badge/KiCad-8.0-blue.svg?logo=kicad)](https://www.kicad.org/)
[![Hardware](https://img.shields.io/badge/Open%20Source-Hardware-green.svg)](https://freedomdefined.org/OSHW)
[![MCU](https://img.shields.io/badge/MCU-STM32F042-orange.svg?logo=stmicroelectronics)](https://www.st.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A practical, standalone 32-bit development board (**26 mm × 36 mm**), inspired by the minimalist philosophy and straightforward nature of the Arduino ATtiny, but optimized for comfortable benchtop development (*devboard*). Powered by the **STM32F042** (ARM Cortex-M0) with native crystal-less USB-C.

---

## 🌟 Why This Project?

This board was born at the intersection of academic learning, curiosity, and maker passion:

1. **Bridging Theory and Practice:** Taking electronic engineering coursework (schematic design, component selection, signal integrity, PCB layout) and applying it to a tangible, physical board.
2. **Stepping into 32-bit Microcontrollers:** Moving beyond traditional 8-bit platforms (AVR, ATtiny) into the modern ARM Cortex ecosystem.
3. **Fun & Hobby:** A passion-driven learning playground to experiment with USB stacks, low-power modes, and embedded programming.
4. **Giving Back to Open Source:** Providing a clean, accessible, and minimal reference design for students, hobbyists, and makers.
5. **Real-World Validation:** Testing and evaluating this hardware throughout the year across real use-cases (relays, OLED menus, battery operation) to confirm that theoretical designs hold up in real life.

---

## ✨ Key Features

* **🧠 Brain:** STMicroelectronics **STM32F042F6P6** (ARM Cortex-M0 @ 48 MHz, 32 KB Flash, 6 KB RAM).
* **🔌 Crystal-less USB-C:** Employs the internal 48 MHz oscillator (`HSI48`) paired with Clock Recovery System (`CRS`) synchronized directly to USB frames—**zero external crystal required**.
* **🚀 Zero-Programmer Flashing (Native DFU):** Factory ROM USB bootloader built-in. Hold the `BOOT` button, plug in the USB-C cable, and flash directly with `STM32CubeProgrammer` or `dfu-util`—no ST-Link or external programmer strictly required!
* **📐 Practical Devboard Layout (26 mm × 36 mm):** Sized for comfortable workbench prototyping, offering generous space for probe clips, jumper wires, clear silkscreen labeling, and uncrowded components.
* **⚡ Pure 3.3V Operation:** On-board low-dropout voltage regulator (LDO) and decoupling capacitors tailored for clean 3.3V logic.
* **🎛️ Dual Tactile Buttons:** Convenient on-board `RESET` and `BOOT0` tactile switches for instant programming mode entry.
* **🛡️ Open-Source & DIY Ready:** Designed with standard 2-layer PCB design rules for affordable fabrication and assembly (e.g. JLCPCB).

---

## 📋 Specifications

| Parameter | Specification |
| :--- | :--- |
| **Microcontroller** | STM32F042F6P6 (TSSOP-20) |
| **Core Architecture** | ARM 32-bit Cortex-M0 @ up to 48 MHz |
| **Flash / SRAM** | 32 KB Flash / 6 KB SRAM |
| **Operating Voltage** | 3.3V DC (Input: 5V via USB-C or external 3.3V rail) |
| **USB Interface** | USB 2.0 Full Speed (12 Mbps) over USB-C |
| **User I/O** | Up to 14 accessible GPIOs (I2C, SPI, USART, PWM, ADC) |
| **Boot Modes** | Native USB DFU in ROM + SWD header pads |
| **Dimensions** | **26 mm × 36 mm** |

---

## 🛠️ Hardware Overview

### Power & Protection
* **USB-C Input:** Standard Type-C receptacle with dual 5.1 kΩ pull-downs on `CC1`/`CC2` for universal charger and PC host compatibility.
* **LDO Regulator:** Low-noise 3.3V regulator powering the MCU and peripherals safely.
* **Decoupling:** Multi-stage high-frequency ceramic capacitors placed directly adjacent to VDD and VDDA pins.

### Signal Routing
* **Differential USB Pair:** Matched $D^+$ and $D^-$ traces routed side-by-side with an unbroken ground reference plane on the bottom layer to maintain high signal integrity.

---

## 💻 Getting Started & Programming

### 1. Entering Native USB DFU Mode
No external probe needed:
1. Hold down the **BOOT** button.
2. Press and release the **RESET** button (or plug the USB-C cable into your PC).
3. Release the **BOOT** button.
4. Your computer now recognizes the device as an **STM32 BOOTLOADER** in DFU mode.

### 2. Flashing
Flash compiled `.bin` or `.hex` firmware using your tool of choice:
* **STM32CubeProgrammer** (GUI / CLI)
* **dfu-util:**
  ```bash
  dfu-util -a 0 -d 0483:df11 --dfuse-address 0x08000000 -D firmware.bin
  ```

### 3. Firmware Support
* **STM32CubeIDE / Keil / IAR:** Native C/C++ development with STM32 HAL / LL drivers.
* **PlatformIO & Arduino:** Fully compatible via the official [STM32duino Core](https://github.com/stm32duino/Arduino_Core_STM32).

---

## 🎯 Yearly Roadmap & Experiments

This repository tracks the ongoing practical validation of the board:
- [x] Schematic design in KiCad 8.
- [x] 2-layer PCB layout with controlled USB differential routing.
- [ ] PCB fabrication and prototype assembly.
- [ ] USB DFU bootloader verification.
- [ ] Experiment 1: Interactive UI menu on 0.96" I2C OLED (SSD1306) using U8g2 page buffer.
- [ ] Experiment 2: Inductive load & relay driver testing (isolated relay control).
- [ ] Experiment 3: Low-power battery operation (LiPo / LiFePO4 direct feed).

---

## 🤝 Contributing & Feedback

Suggestions, questions, and PRs are very welcome! Whether you are a student exploring embedded design or an experienced engineer with layout tips, feel free to open an **Issue** or submit a **Pull Request**.

---

## 📜 License

This project is licensed under the [MIT License](LICENSE) - feel free to build, modify, and learn from it!
