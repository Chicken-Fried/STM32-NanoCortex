<div align="center">

# ⚡ NanoCortex-F042

**Minimalist ARM Cortex-M0 development board — 20 mm × 38.5 mm, native USB-C, crystal-less**

[![KiCad](https://img.shields.io/badge/KiCad-10.0-blue.svg?logo=kicad)](https://www.kicad.org/)
[![Hardware](https://img.shields.io/badge/Open%20Source-Hardware-green.svg)](https://freedomdefined.org/OSHW)
[![MCU](https://img.shields.io/badge/MCU-STM32F042-orange.svg?logo=stmicroelectronics)](https://www.st.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[🇫🇷 Version française](README_FR.md) · [📄 Schematic (PDF)](arm_tiny_pcb_sch.pdf) · [🧰 Getting started](#getting-started) · [📌 Pinout](#pinout)

<img src="docs/board_3d.jpg" alt="NanoCortex-F042 top view" height="430"> <img src="docs/board_3d_iso.jpg" alt="NanoCortex-F042 3D perspective" height="430">

</div>

---

A practical, standalone 32-bit development board (**20 mm × 38.5 mm**), inspired by the minimalist philosophy and straightforward nature of the Arduino ATtiny, but optimized for comfortable benchtop development (*devboard*). Powered by the **STM32F042** (ARM Cortex-M0) with native crystal-less USB-C, a **TVS-protected** USB input and a **ceramic-only 3.3 V power stage**.

---

## 🌟 Why This Project?

This board was born at the intersection of academic learning, curiosity, and maker passion:

1. **Bridging Theory and Practice:** Taking electronic engineering coursework (schematic design, component selection, signal integrity, PCB layout) and applying it to a tangible, physical board.
2. **Stepping into 32-bit Microcontrollers:** Moving beyond traditional 8-bit platforms (AVR, ATtiny) into the modern ARM Cortex ecosystem.
3. **Fun & Hobby:** A passion-driven learning playground to experiment with USB stacks, low-power modes, and embedded programming.
4. **Giving Back to Open Source:** Providing a clean, accessible, and minimal reference design for students, hobbyists, and makers.
5. **Real-World Project Stepping Stone:** Serving as the core validation platform for three concrete engineering builds: a dedicated **drone telemetry/control subsystem**, an **audio synthesizer with active analog op-amp (AOP) filtering**, and a **digitally controlled $\ge$ 40W USB-PD / Buck converter power stage**.

---

## ✨ Key Features

* **🧠 Brain:** STMicroelectronics **STM32F042F6P6** (ARM Cortex-M0 @ 48 MHz, 32 KB Flash, 6 KB RAM).
* **🔌 Crystal-less USB-C:** Employs the internal 48 MHz oscillator (`HSI48`) paired with Clock Recovery System (`CRS`) synchronized directly to USB frames—**zero external crystal required**.
* **🚀 Zero-Programmer Flashing (Native DFU):** Factory ROM USB bootloader built-in. Hold the `BOOT` button, plug in the USB-C cable, and flash directly with `STM32CubeProgrammer` or `dfu-util`—no ST-Link or external programmer strictly required!
* **📐 Compact Devboard Layout (20 mm × 38.5 mm):** Slim, breadboard-friendly format with two 9-pin I/O headers on the long sides, and the `BOOT` / `RESET` buttons on each side of the USB-C connector.
* **🛡️ Enhanced USB Protection:** **SD05-01FTG** TVS diode on `VBUS`, **USBLC6-2SC6** on the data lines and a 500 mA resettable polyfuse.
* **⚡ Stable 3.3 V:** **ME6211C33M5G-N** low-dropout, low-quiescent-current LDO, stable with small **ceramic capacitors** (no more tantalum).
* **💡 Two Indicator LEDs:** a red `3V3` power LED and an addressable **SK6805-EC20** RGB `STATUS` LED driven from `PA0`.
* **🎛️ Dual Tactile Buttons:** On-board `RESET` and `BOOT` tactile switches for instant programming mode entry.
* **🛠️ Open-Source & DIY Ready:** Standard 2-layer PCB design rules for affordable fabrication and assembly (e.g. JLCPCB).

---

## 📋 Specifications

| Parameter | Specification |
| :--- | :--- |
| **Microcontroller** | STM32F042F6P6 (TSSOP-20) |
| **Core Architecture** | ARM 32-bit Cortex-M0 @ up to 48 MHz |
| **Flash / SRAM** | 32 KB Flash / 6 KB SRAM |
| **Operating Voltage** | 3.3 V logic (input: 5 V via USB-C) |
| **3.3 V Regulator** | ME6211C33M5G-N (LDO, SOT-23-5) with 2 ceramic capacitors (X7R, 25 V, 0805) |
| **Input Protection** | SD05-01FTG (TVS) + USBLC6-2SC6 (USB data lines) + 500 mA polyfuse |
| **USB Interface** | USB 2.0 Full Speed (12 Mbps) over USB-C |
| **User I/O** | 13 GPIOs on 2.54 mm headers (I2C, SPI, USART, PWM, ADC) |
| **Programming** | Native USB DFU (ROM bootloader) or SWD on `PA13` / `PA14` |
| **On-board LEDs** | Red `3V3` power LED + SK6805-EC20 RGB status LED (`PA0`) |
| **Dimensions** | **20 mm × 38.5 mm** |

---

<a id="pinout"></a>
## 📌 Pinout

The board has two 9-pin headers (`J1` on the left, `J2` on the right) and a 2 × 2 power header (`J3`) at the bottom edge.

| Header | Pin | Signal | MCU pin | Notes |
| :---: | :---: | :--- | :--- | :--- |
| **J1** | 1 | `3V3` | – | 3.3 V rail |
| | 2 | `GPIO1` | `PB8` | Shared with `BOOT0` (10 kΩ pull-down) |
| | 3 | `GPIO2` | `PF0` | |
| | 4 | `GPIO3` | `PF1` | |
| | 5 | `GPIO5` | `PA1` | |
| | 6 | `GPIO6` | `PA2` | |
| | 7 | `GPIO7` | `PA3` | |
| | 8 | `GPIO8` | `PA4` | |
| | 9 | `GND` | – | |
| **J2** | 1 | `3V3` | – | 3.3 V rail |
| | 2 | `GPIO9` | `PA5` | |
| | 3 | `GPIO10` | `PA6` | |
| | 4 | `GPIO11` | `PA7` | |
| | 5 | `GPIO12` | `PB1` | |
| | 6 | `GND` | – | |
| | 7 | `GND` | – | |
| | 8 | `GPIO15` | `PA13` | `SWDIO` |
| | 9 | `GPIO16` | `PA14` | `SWCLK` |
| **J3** | 1–4 | `3V3` / `GND` | – | 2 × 2 header: 2 × `3V3`, 2 × `GND` (power breakout) |

> **Internal signals:** `PA0` → SK6805 status LED data · `NRST` → `RESET` button + 10 kΩ pull-up + 100 nF · `BOOT0` → `BOOT` button.
>
> **USB pins:** on the TSSOP-20 package, USB `D-` / `D+` use pins 17 / 18 (`PA11` / `PA12` remapped from `PA9` / `PA10`). See the STM32F042 reference manual (`SYSCFG_CFGR1`, `PA11_PA12_RMP`).

---

## 🛠️ Hardware Overview

[![NanoCortex-F042 schematic — click for the full-resolution PDF](docs/schematic_preview.png)](arm_tiny_pcb_sch.pdf)

> 🔎 **Click the schematic to open the full-resolution vector PDF** → [`arm_tiny_pcb_sch.pdf`](arm_tiny_pcb_sch.pdf)

### Power & Protection
* **USB-C Input:** Standard Type-C receptacle (GT-USB-7025) with dual 5.1 kΩ pull-downs on `CC1`/`CC2` for universal charger and PC host compatibility.
* **TVS Diode (SD05-01FTG, D1):** Clamps ESD and surge events on `VBUS` (5 V) before they can reach the rest of the board.
* **Polyfuse (F1, 500 mA):** Resettable fuse between `VBUS` and the 5 V rail.
* **USB Data Protection (USBLC6-2SC6, U3):** Low-capacitance ESD protection on `D+` / `D-`, preserving Full-Speed signal integrity.
* **LDO Regulator (ME6211C33M5G-N, LDO1):** 5 V → 3.3 V, low dropout and very low quiescent current.
* **Ceramic-Only Capacitors:** Tantalum capacitors were replaced by **X7R ceramic capacitors** (`C1` 2.2 µF, `C2` 1 µF, 25 V, 0805) around the regulator: more stable with this LDO, smaller, non-polarized, and free of tantalum failure modes (inrush / surge).
* **Decoupling:** `C3` 100 nF, `C4` 4.7 µF, `C5` 10 nF and `C6` 1 µF placed close to the `VDD` / `VDDA` pins.

### Signal Routing
* **Differential USB Pair:** Matched $D^+$ and $D^-$ traces routed side-by-side with an unbroken ground reference plane on the bottom layer to maintain high signal integrity.

---

## 🧾 Key Components

| Ref | Part | Function |
| :--- | :--- | :--- |
| U1 | STM32F042F6P6 | Microcontroller (TSSOP-20) |
| LDO1 | ME6211C33M5G-N | 3.3 V LDO regulator (SOT-23-5) |
| U3 | USBLC6-2SC6 | ESD protection for USB data lines |
| D1 | SD05-01FTG | 5 V TVS diode on `VBUS` (SOD-323) |
| F1 | JK-SMD0603-050-6 | 0603 resettable fuse (500 mA) |
| USB1 | GT-USB-7025 | USB Type-C receptacle |
| SW1 / SW2 | SKRKAEE020 | `RESET` / `BOOT` tactile switches |
| LED1 | 16-213/BHC-AN1P2/3T | Red `3V3` power LED |
| LED2 | SK6805-EC20 | RGB `STATUS` LED (addressable) |
| J1 / J2 / J3 | 1×9 / 1×9 / 2×2 pin headers | I/O and power headers |

---

## 📝 Revision History

| Change | Before | Now |
| :--- | :--- | :--- |
| **Board size** | 26 mm × 36 mm | **20 mm × 38.5 mm** |
| **LDO regulator** | XBL1117-3.3 (SOT-89) | **ME6211C33M5G-N** (SOT-23-5) |
| **Regulator capacitors** | Tantalum (EIA-3528) | **X7R ceramic (0805)** |
| **5 V input protection** | Fuse only | Fuse + **SD05-01FTG TVS diode** |

---

<a id="getting-started"></a>
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
* **SWD (optional):** connect an ST-Link to `GND`, `3V3`, `PA13` (`SWDIO`) and `PA14` (`SWCLK`) on `J1` / `J2`.

### 3. Firmware Support
* **STM32CubeIDE / Keil / IAR:** Native C/C++ development with STM32 HAL / LL drivers.
* **PlatformIO & Arduino:** Fully compatible via the official [STM32duino Core](https://github.com/stm32duino/Arduino_Core_STM32).

---

## 📁 Repository Content

| File / Folder | Description |
| :--- | :--- |
| [`arm_tiny_pcb.kicad_pro`](arm_tiny_pcb.kicad_pro) | KiCad project (open this one) |
| [`arm_tiny_pcb.kicad_sch`](arm_tiny_pcb.kicad_sch) | KiCad schematic |
| [`arm_tiny_pcb.kicad_pcb`](arm_tiny_pcb.kicad_pcb) | KiCad PCB layout |
| [`arm_tiny_pcb_sch.pdf`](arm_tiny_pcb_sch.pdf) | Schematic export (PDF) |
| [`arm_tiny_pcb.jpg`](arm_tiny_pcb.jpg) | 3D render of the board (full size) |
| [`docs/`](docs) | Images used in this README (top view, 3D perspective, schematic preview) |
| [`NanoCortex.kicad_sym`](NanoCortex.kicad_sym) | Project symbol library |
| [`NanoCortex.pretty/`](NanoCortex.pretty) | Project footprint library |
| [`NanoCortex.3dshapes/`](NanoCortex.3dshapes) | 3D models (`.wrl`) for the project footprints |
| `sym-lib-table`, `fp-lib-table` | Project library tables (paths relative to the project) |

> 📦 **Libraries:** everything needed to open the project is included. The `NanoCortex` libraries are registered automatically when you open `arm_tiny_pcb.kicad_pro` with **KiCad 10**.

---

## 🎯 Roadmap & Target Application Projects

This board serves as the prototyping brain for three dedicated embedded hardware projects:

### 🛸 Track 1: Lightweight Drone Subsystem & Telemetry Board
Using the NanoCortex-F042 as an embedded flight module or motor/sensor companion node:
- [ ] **Sensor Interface:** High-rate 6-axis IMU (gyro/accelerometer via SPI/I2C) readout on hardware timer interrupts.
- [ ] **Actuator Control:** Multi-channel high-speed motor control signals (OneShot / DShot / PWM at 400 Hz+).
- [ ] **Telemetry & Communication:** Real-time bi-directional link over UART (CRSF / SBUS / MSP protocol) or CAN bus.
- [ ] **Custom PCB Spin:** Layout of a dedicated, miniaturized drone PCB integrating motor drivers and power management.

### 🎛️ Track 2: Hybrid USB-MIDI Synthesizer & Analog Op-Amp Audio Lab
A hands-on project to master operational amplifiers (Op-Amps / AOP) and USB communication without requiring heavy DSP:
- [ ] **USB-MIDI Communication:** Native class-compliant USB-MIDI device stack (plug-and-play with DAWs, keyboards, and PCs with zero drivers).
- [ ] **Sound Generation:** Multi-waveform oscillator (sawtooth, square, triangle, wavetable) generated via high-frequency hardware PWM / DMA.
- [ ] **Active Op-Amp Reconstruction Filter:** 2nd- or 4th-order active low-pass filter (Sallen-Key / Rauch topology) to smooth PWM into clean analog audio.
- [ ] **Analog Processing & Overdrive Stage:** Soft-clipping diode distortion stage within the op-amp feedback loop (classic overdrive pedal architecture) with active gain control.
- [ ] **Active Tone Control & Output Stage:** Active Baxandall bass/treble tone stack and low-impedance audio buffer for headphones or line-level output.

### ⚡ Track 3: Digitally-Controlled Buck Converter & 40W+ USB-PD Lab
A hands-on power electronics project to master switch-mode power supplies (Buck converters), op-amp feedback injection, and USB Power Delivery:
- [ ] **Synchronous Buck Stage:** Design of an external 24 V DC → 5 V–20 V / 3 A step-down converter (MOSFET selection, inductor saturation $I_{sat}$, and low-ESR ripple filtering).
- [ ] **Op-Amp Feedback Injection:** Dynamic voltage margin/target control via active op-amp summing into the Buck controller's feedback (`FB`) node.
- [ ] **USB-PD PHY Communication (FUSB302B):** I2C control of a dedicated USB-PD Source controller to negotiate 5 V, 9 V, 15 V, and 20 V profiles with laptops and phones.
- [ ] **Power Telemetry & Safety:** Real-time $V_{out}$ / $I_{out}$ monitoring via STM32 12-bit ADC, over-current/over-voltage shutdown, and $V_{BUS}$ power-switch control.

### 🧪 Board Validation Milestones
- [x] KiCad 10 schematic design & 2-layer PCB layout with matched USB differential pairs.
- [x] Hardware Revision: 20 mm × 38.5 mm form factor, TVS protection diode, ME6211 LDO, and MLCC ceramic capacitors.
- [ ] PCB fabrication and prototype SMD assembly.
- [ ] USB DFU bootloader and crystal-less CRS clock verification.
- [ ] 3.3 V power rail validation (ripple, stability, and transient response under load).

---

## 🤝 Contributing & Feedback

Suggestions, questions, and PRs are very welcome! Whether you are a student exploring embedded design or an experienced engineer with layout tips, feel free to open an **Issue** or submit a **Pull Request**.

---

## 📜 License

This project is licensed under the [MIT License](LICENSE) - feel free to build, modify, and learn from it!
