<div align="center">

<img src="https://capsule-render.vercel.app/api?type=venom&color=0:8B0000,50:C1121F,100:FFB300&height=200&section=header&text=PARSHWA%20SANGAME&fontSize=48&fontColor=FFFFFF&animation=fadeIn&fontAlignY=38&desc=Embedded%20Systems%20%7C%20Hardware%20%7C%20Research&descAlignY=58&descSize=18" />

</div>

<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=800&color=00D4FF&center=true&vCenter=true&width=700&lines=SYSTEM+INITIALIZING...;LOADING+SUIT+LOG...;WELCOME.+SYSTEMS+ONLINE.;FOUR+SENSORS+ONLINE.+PREDICTIVE+MAINTENANCE+ACTIVE." alt="boot sequence" />

</div>

<p align="center">
  <img src="https://img.shields.io/badge/STATUS-ALL%20SYSTEMS%20ONLINE-FFB300?style=for-the-badge&labelColor=8B0000" />
  <img src="https://img.shields.io/badge/CORE-STM32F446RE-00D4FF?style=for-the-badge&labelColor=1a1a1a" />
  <img src="https://img.shields.io/badge/FIRMWARE-BARE--METAL-C1121F?style=for-the-badge&labelColor=1a1a1a" />
</p>

---

## // SYSTEM OVERVIEW

Final-year Electronics and Communication Engineering student, Bangalore. I build embedded hardware, sensing systems, firmware, and the analog circuitry that lets a machine tell you it is about to fail before it does. Alongside engineering, I run independent research on where new hardware opportunities are emerging across Indian industry.

Think of it as building my own suit, one system at a time. Not a weapon. A machine that watches other machines and warns you first.

- 🔧 Currently building: four-sensor predictive maintenance node with a live dashboard, STM32
- ⚡ Currently calibrating: RTOS and CAN bus fundamentals
- 🎯 Target sectors: industrial automation, EV and battery systems, IoT hardware
- 📡 Comms channel: **sangame.parshwa@gmail.com**

---

## // SUIT LOG

### 🔴🟡 MARK I — Predictive Maintenance Edge Node
**[github.com/sangameparshwa-sudo/stm32-predictive-maintenance](https://github.com/sangameparshwa-sudo/stm32-predictive-maintenance)**
*Flagship build. Full suit online.*

<p>
  <img src="https://img.shields.io/badge/STATUS-4%2F4%20SENSORS%20ONLINE-00C853?style=flat-square&labelColor=1a1a1a" />
  <img src="https://img.shields.io/badge/CORE-STM32F446RE-00D4FF?style=flat-square&labelColor=1a1a1a" />
  <img src="https://img.shields.io/badge/MODE-BARE--METAL-C1121F?style=flat-square&labelColor=1a1a1a" />
</p>

A device built to catch machine faults before they cause failure. Four sensors feed a single STM32 across ADC, SPI, and 1-Wire. Every cycle, each sensor is reduced to one feature, current, vibration, sound, and temperature, streamed live and read against thresholds that adapt to the machine they are watching.

**// DIAGNOSTIC PANEL**

| Subsystem | Sensor | Bus | Status |
|---|---|---|---|
| Current sensing | SCT-013 CT | ADC | 🟢 ONLINE, sum-of-squares RMS |
| Vibration sensing | ADXL345 | SPI | 🟢 ONLINE, RMS of acceleration magnitude |
| Acoustic sensing | MAX4466 mic | ADC | 🟢 ONLINE, RMS level |
| Temperature sensing | DS18B20 | 1-Wire, bit-banged (TIM2) | 🟢 ONLINE |

**// BUILD NOTES**

- Designed a custom analog front end for the current transformer. A 1.65V active DC-bias network centers the AC signal inside the ADC's input range.
- Computed true RMS by sum of squares, not peak detection, for every analog channel. An earlier peak-to-peak method produced phantom readings under electrical noise. Rebuilding the math to sum-of-squares was the single biggest accuracy fix in the whole system.
- Streamed all four features live over USART2 to USB at 115200 baud, feeding a PC-side dashboard in real time.
- Built the architecture non-blocking, so the slow DS18B20 conversion never stalls the fast analog sensors.
- Enabled the FPU for floating-point RMS math. Skipping this step causes a silent HardFault, one of the harder bugs to trace on bare metal.
- Star-grounded the board, separate analog and digital grounds, to cut noise coupling between channels.
- Fixed a C-runtime startup issue (CubeIDE Empty Project versus a hand-rolled setup) that was breaking debugger visibility.

**// INTELLIGENCE LAYER**

- **Manual mode:** enter the motor's horsepower, and thresholds auto-set from NEC full-load-current tables.
- **Learn mode:** baselines a healthy motor for up to 10 minutes, then sets thresholds statistically at mean plus 3-sigma for warning and plus 5-sigma for trip.
- **Priority-ordered alarms:** vibration, then temperature, then current, then acoustic, since acoustic is the noisiest and least trusted signal.
- **CSV export** for logging and offline analysis. **Sensor-range awareness** warns if the entered motor size exceeds the current clamp's rated range.

> **⚠️ HONESTY LOG, read before you trust this system:** Learn mode is adaptive **statistical** anomaly detection (mean + k-sigma), not a trained ML model, and it is described that way on purpose. Current and temperature thresholds are grounded in real standards. Vibration and acoustic thresholds are placeholders until baselined on an actual motor. The whole system is assembled on breadboard right now; perfboard or a soldered build is the next step before this leaves the bench.

**// GROUND CONTROL (PC-side)**

- `bridge.py`, a Python serial-to-browser bridge that reads the UART stream and serves live JSON plus a dashboard over HTTP.
- `pdm_dashboard_live.html`, an industrial-style HMI: real-time gauges, a feature-history scope, a live radar signature plot, and escalating Normal, Warning, and Critical states. Reachable from a phone over local WiFi.

**// REPO CONTENTS:** `four_sensor_uart_full.c` (main firmware) · `bridge.py` · `pdm_dashboard_live.html` · standalone sensor tests (`adxl_test.c`, `mic_test.c`, `ds18b20_test.c`, `i2c_scanner.c`) · wiring docs (`PdM_Connections.pdf`, `pdm_circuit_diagram.png/svg/pdf`)

**// NEXT DEPLOYMENT:** baseline vibration and acoustic thresholds on a real motor, then move the build off breadboard onto perfboard for a lower noise floor.

---

### 🟡 MARK II — ML-Based Smart Billing Cart
**[github.com/sangameparshwa-sudo/automatic-smart-billing-cart-esp32](https://github.com/sangameparshwa-sudo/automatic-smart-billing-cart-esp32)**

A cart that bills items in real time as they are added. An ESP32-CAM recognizes each product through the camera, inference running entirely on-device, no cloud dependency. Led technical coordination across a 4-member crew, task allocation to integration checkpoints, delivered on schedule.

`ESP32-CAM` `Edge Impulse` `Embedded ML`

### 🔵 MARK III — Opportunity Research, India
**[github.com/sangameparshwa-sudo/opportunity-research-india](https://github.com/sangameparshwa-sudo/opportunity-research-india)**

Independent intelligence gathering. Tracking emerging hardware and manufacturing opportunities across Indian industry, demand drivers, supply chain structures, and where technical gaps still exist. Built from trade exhibitions and ground observation, not headlines.

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
| **Interfaces** | I2C, SPI, UART, ADC (multi-channel scanning), 1-Wire |
| **Hardware** | Analog signal conditioning, current sensing, sensor integration, component selection |
| **Software / Tools** | STM32CubeIDE, Arduino IDE, LabVIEW, Edge Impulse, Python, Git/GitHub |

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
