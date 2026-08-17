<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=24&pause=1000&color=2E9EF7&center=true&vCenter=true&width=600&lines=Hi%2C+I'm+Parshwa+Sangame;Final-Year+ECE+Student%2C+Bangalore;I+build+embedded+hardware;Currently%3A+Predictive+Maintenance+Edge+Node" alt="Typing SVG" />

</div>

<p align="center">
  <img src="https://img.shields.io/badge/STM32-03234B?style=for-the-badge&logo=stmicroelectronics&logoColor=white" />
  <img src="https://img.shields.io/badge/Embedded_C-00599C?style=for-the-badge&logo=c&logoColor=white" />
  <img src="https://img.shields.io/badge/ARM_Cortex--M-0091BD?style=for-the-badge&logo=arm&logoColor=white" />
  <img src="https://img.shields.io/badge/ESP32-E7352C?style=for-the-badge&logo=espressif&logoColor=white" />
</p>

## About Me

I am a final-year Electronics and Communication Engineering student in Bangalore. I build embedded hardware, and my work sits at the sensing and firmware layer, from analog front end design to bring-up and debugging on live hardware. Alongside engineering, I do independent research on where new hardware opportunities are emerging across Indian industry.

- Building a four-sensor predictive maintenance node on STM32
- Currently strengthening RTOS and CAN bus fundamentals
- Interested in industrial automation, EV and battery systems, and IoT hardware
- Reach me: **sangame.parshwa@gmail.com**

---

## Featured Project

### 🔧 Predictive Maintenance Edge Node
**[github.com/sangameparshwa-sudo/stm32-predictive-maintenance](https://github.com/sangameparshwa-sudo/stm32-predictive-maintenance)**

<p>
  <img src="https://img.shields.io/badge/Status-In%20Progress-yellow?style=flat-square" />
  <img src="https://img.shields.io/badge/Platform-STM32F446RE-blue?style=flat-square" />
  <img src="https://img.shields.io/badge/Firmware-Bare--Metal-orange?style=flat-square" />
</p>

A device built to catch machine faults before they cause failure. Four sensors feed a single STM32 across three buses. Every cycle, each sensor is reduced to one feature current, sound, vibration, and temperature, and together those features describe the machine's health. The firmware runs bare-metal at register level, with all peripheral drivers integrated directly.

**Sensor status:**

| Subsystem | Sensor | Bus | Status |
|---|---|---|---|
| Current sensing | SCT-013-030 CT | ADC (multi-channel) | ✅ Verified and calibrated |
| Acoustic sensing | MAX4466 mic amp | ADC (multi-channel) | ✅ Working |
| Vibration sensing | ADXL345 | SPI1 (Mode 3) | ✅ Working |
| Thermal sensing | MLX90614 IR | I2C1 (SMBus) | 🟡 In progress, physical connection fault diagnosed |

**What went into it:**

- Designed a custom analog front end for the current transformer: a 1.65V active DC-bias network that centers the AC signal inside the ADC's input range, with decoupling to isolate supply ripple.
- Computed true RMS current by sum of squares with per-window DC offset removal. An earlier peak-to-peak method produced phantom readings under electrical noise. Diagnosing that and switching to sum of squares was the single biggest accuracy fix in the project.
- Chose SPI over I2C for the vibration sensor, for faster data and to keep the I2C bus free for the thermal sensor. Bring-up verifies the DEVID register reads 0xE5 before trusting any data.
- Take the RMS of acceleration magnitude about its mean, so gravity and mounting orientation cancel out of the vibration feature.
- Added bounded timeouts to the I2C driver, so a faulty sensor flags an error instead of hanging the whole node. That design choice is proving itself right now, since the thermal channel is currently down and the other three keep running normally.
- Own the build end to end: component selection, BOM, vendor sourcing, and phased integration with validation at each stage.

**Next:** fix the thermal channel's physical connection, then build the anomaly detection layer over the feature vector.

---

## Other Projects

### 🛒 ML-Based Smart Billing Cart
**[github.com/sangameparshwa-sudo/automatic-smart-billing-cart-esp32](https://github.com/sangameparshwa-sudo/automatic-smart-billing-cart-esp32)**

A shopping cart that bills items in real time as they are added. An ESP32-CAM recognizes each product through the camera, with inference running entirely on-device via Edge Impulse, no cloud dependency. Led technical coordination across a 4-member team, from task allocation to integration checkpoints, and delivered on schedule.

`ESP32-CAM` `Edge Impulse` `Embedded ML`

### 📊 Opportunity Research, India
**[github.com/sangameparshwa-sudo/opportunity-research-india](https://github.com/sangameparshwa-sudo/opportunity-research-india)**

Independent research tracking emerging hardware and manufacturing opportunities across Indian industry: demand drivers, supply chain structures, and where technical gaps still exist. Built from trade exhibitions and ground observation, not headlines.

`Industrial Automation` `EV & Battery Systems` `Renewable Energy` `Smart Hardware`

---

## Tech Stack

<p align="left">
  <img src="https://skillicons.dev/icons?i=c,arduino,git,github" />
</p>

**Languages:** Embedded C, C
**Firmware:** Bare-metal register-level programming, STM32 HAL, peripheral driver integration, hardware bring-up and debugging
**Platforms:** ARM Cortex-M4 (STM32 Nucleo-F446RE), ESP32 / ESP32-CAM, 32-bit microcontrollers
**Interfaces:** I2C, SPI, UART, ADC (multi-channel scanning)
**Hardware:** Analog signal conditioning, current sensing, sensor integration, component selection
**Tools:** STM32CubeIDE, Arduino IDE, LabVIEW, Edge Impulse, Git/GitHub

**Currently strengthening:** RTOS fundamentals (tasks, scheduler, preemption, queues/semaphores), CAN bus fundamentals (differential signaling, message-based arbitration), BMS architecture, PCB design (KiCad)

---

## Certifications

- Advanced C Programming, Microchip Technology Inc.
- ARM Cortex-M, Pyjama Cafe
- Getting Started with AI, IBM SkillsBuild

---

<div align="center">

<a href="https://in.linkedin.com/in/parshwa-sangame-a89484314">
  <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" />
</a>
<a href="mailto:sangame.parshwa@gmail.com">
  <img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" />
</a>

<img src="https://komarev.com/ghpvc/?username=sangameparshwa-sudo&label=Profile+Views&color=2E9EF7&style=flat" alt="profile views" />

</div>
