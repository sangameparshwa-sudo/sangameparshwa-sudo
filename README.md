<div align="center">

<img src="https://capsule-render.vercel.app/api?type=venom&color=0:8B0000,50:C1121F,100:FFB300&height=200&section=header&text=PARSHWA%20SANGAME&fontSize=48&fontColor=FFFFFF&animation=fadeIn&fontAlignY=38&desc=Embedded%20Systems%20%7C%20Hardware%20%7C%20Research&descAlignY=58&descSize=18" />

</div>

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=800&color=00D4FF&center=true&vCenter=true&width=700&lines=SYSTEM+INITIALIZING...;LOADING+SUIT+LOG...;WELCOME.+SYSTEMS+ONLINE.;BUILDING%3A+PREDICTIVE+MAINTENANCE+EDGE+NODE" alt="boot sequence" />

</div>

<p align="center">
  <img src="https://img.shields.io/badge/STATUS-ONLINE-FFB300?style=for-the-badge&labelColor=8B0000" />
  <img src="https://img.shields.io/badge/CORE-STM32F446RE-00D4FF?style=for-the-badge&labelColor=1a1a1a" />
  <img src="https://img.shields.io/badge/FIRMWARE-BARE--METAL-C1121F?style=for-the-badge&labelColor=1a1a1a" />
</p>

---

## // SYSTEM OVERVIEW

Final-year Electronics and Communication Engineering student, Bangalore. I build embedded hardware, sensing systems, firmware, and the analog circuitry that lets a machine tell you it is about to fail before it does. Alongside engineering, I run independent research on where new hardware opportunities are emerging across Indian industry.

Think of it as building my own suit, one system at a time. Not a weapon. A machine that watches other machines and warns you first.

- 🔧 Currently building: four-sensor predictive maintenance node, STM32
- ⚡ Currently calibrating: RTOS and CAN bus fundamentals
- 🎯 Target sectors: industrial automation, EV and battery systems, IoT hardware
- 📡 Comms channel: **sangame.parshwa@gmail.com**

---

## // SUIT LOG

### 🔴🟡 MARK I — Predictive Maintenance Edge Node
**[github.com/sangameparshwa-sudo/stm32-predictive-maintenance](https://github.com/sangameparshwa-sudo/stm32-predictive-maintenance)**
*Flagship build. Primary system online.*

<p>
  <img src="https://img.shields.io/badge/STATUS-CALIBRATING-FFB300?style=flat-square&labelColor=1a1a1a" />
  <img src="https://img.shields.io/badge/CORE-STM32F446RE-00D4FF?style=flat-square&labelColor=1a1a1a" />
  <img src="https://img.shields.io/badge/MODE-BARE--METAL-C1121F?style=flat-square&labelColor=1a1a1a" />
</p>

A device built to catch machine faults before they cause failure. Four sensors feed a single STM32 across three buses. Every cycle, each sensor is reduced to one feature, current, sound, vibration, and temperature, and together those features describe the machine's health in real time. All firmware runs bare-metal at register level.

**// DIAGNOSTIC PANEL**

| Subsystem | Sensor | Bus | Status |
|---|---|---|---|
| Current sensing | SCT-013-030 CT | ADC (multi-channel) | 🟢 ONLINE, verified and calibrated |
| Acoustic sensing | MAX4466 mic amp | ADC (multi-channel) | 🟢 ONLINE |
| Vibration sensing | ADXL345 | SPI1 (Mode 3) | 🟢 ONLINE |
| Thermal sensing | MLX90614 IR | I2C1 (SMBus) | 🟡 CALIBRATING, physical fault diagnosed |

**// BUILD NOTES**

- Designed a custom analog front end for the current transformer. A 1.65V active DC-bias network centers the AC signal inside the ADC's input range, with decoupling to isolate supply ripple.
- Computed true RMS current by sum of squares with per-window DC offset removal. An earlier peak-to-peak method produced phantom readings under electrical noise. Diagnosing that and rebuilding the math was the single biggest accuracy fix in the whole system.
- Chose SPI over I2C for the vibration sensor, for faster data and to keep the I2C bus free. Bring-up verifies the DEVID register reads 0xE5 before trusting any data.
- Take the RMS of acceleration magnitude about its mean, so gravity and mounting orientation cancel out of the vibration feature.
- Added bounded timeouts to the I2C driver, so a faulty sensor flags an error instead of taking the whole node down with it. That design call is proving itself right now. Thermal is down, and the other three systems keep running clean.
- Own the build end to end: component selection, BOM, vendor sourcing, and phased integration with validation at each stage.

**// NEXT DEPLOYMENT:** fix the thermal channel's physical connection, then bring the anomaly detection layer online over the feature vector.

---

### 🟡 MARK II — ML-Based Smart Billing Cart
**[github.com/sangameparshwa-sudo/automatic-smart-billing-cart-esp32](https://github.com/sangameparshwa-sudo/automatic-smart-billing-cart-esp32)**

A cart that bills items in real time as they are added. An ESP32-CAM recognizes each product through the camera, inference running entirely on-device, no cloud dependency. Led technical coordination across a 4-member crew, task allocation to integration checkpoints, delivered on schedule.

`ESP32-CAM` `Edge Impulse` `Embedded ML`

### 🔵 MARK III — Opportunity Research, India
**[github.com/sangameparshwa-sudo/opportunity-research-india](https://github.com/sangameparshwa-sudo/opportunity-research-india)**

Independent intelligence gathering. Tracking emerging hardware and manufacturing opportunities across Indian industry: demand drivers, supply chain structures, and where technical gaps still exist. Built from trade exhibitions and ground observation, not headlines.

`Industrial Automation` `EV & Battery Systems` `Renewable Energy` `Smart Hardware`

---

## // CORE SYSTEMS

<p align="left">
  <img src="https://skillicons.dev/icons?i=c,arduino,git,github&theme=dark" />
</p>

| Layer | Loadout |
|---|---|
| **Languages** | Embedded C, C |
| **Firmware** | Bare-metal register-level programming, STM32 HAL, peripheral driver integration, hardware bring-up and debugging |
| **Platforms** | ARM Cortex-M4 (STM32 Nucleo-F446RE), ESP32 / ESP32-CAM, 32-bit microcontrollers |
| **Interfaces** | I2C, SPI, UART, ADC (multi-channel scanning) |
| **Hardware** | Analog signal conditioning, current sensing, sensor integration, component selection |
| **Tools** | STM32CubeIDE, Arduino IDE, LabVIEW, Edge Impulse, Git/GitHub |

**// SYSTEMS IN CALIBRATION:** RTOS fundamentals (tasks, scheduler, preemption, queues/semaphores) · CAN bus fundamentals (differential signaling, message-based arbitration) · BMS architecture · PCB design (KiCad)

---

## // CERTIFIED PROTOCOLS

- Advanced C Programming, Microchip Technology Inc.
- ARM Cortex-M, Pyjama Cafe
- Getting Started with AI, IBM SkillsBuild

---

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=sangameparshwa-sudo&show_icons=true&theme=dark&title_color=FFB300&icon_color=00D4FF&text_color=FFFFFF&bg_color=0D1117&border_color=C1121F&hide_border=false" />

</div>

<div align="center">

<a href="https://in.linkedin.com/in/parshwa-sangame-a89484314">
  <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" />
</a>
<a href="mailto:sangame.parshwa@gmail.com">
  <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" />
</a>

<br><br>

<img src="https://komarev.com/ghpvc/?username=sangameparshwa-sudo&label=SYSTEM+SCANS&color=C1121F&style=for-the-badge" alt="profile views" />

<img src="https://capsule-render.vercel.app/api?type=venom&color=0:FFB300,50:C1121F,100:8B0000&height=100&section=footer" />

</div>
