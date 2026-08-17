# PdM Edge Node — Multi-Sensor Predictive Maintenance

A bare-metal STM32 system that monitors an electric motor's health in real time using four sensors across four communication protocols. It streams live data to a browser or mobile dashboard with adaptive, statistics-based anomaly detection.

## Overview

The node reads current, vibration, acoustic, and temperature data from a running motor, computes RMS features on-device, and streams them over UART to a PC. A Python bridge serves a live dashboard accessible from any phone or laptop on the same WiFi. Thresholds can be set manually from motor ratings or learned automatically by baselining a healthy motor.

## Hardware / Firmware

Target: STM32F446RE, bare-metal C (register-level, no HAL).

- **Current** — SCT-013 current transformer on ADC, 1.65V bias front-end, sum-of-squares RMS
- **Vibration** — ADXL345 3-axis accelerometer over SPI, RMS of acceleration magnitude
- **Acoustic** — MAX4466 microphone on ADC, RMS level
- **Temperature** — DS18B20 probe over 1-Wire, bit-banged with microsecond timing via TIM2
- Four protocols in one node: ADC ×2, SPI, 1-Wire
- All four features streamed over USART2 to USB at 115200 baud
- Non-blocking architecture — the slow DS18B20 conversion does not stall the fast sensors
- FPU enabled for floating-point RMS math
- Star-grounding — separate analog and digital grounds to reduce noise coupling

## Software (PC side)

- **Python bridge** — reads the serial stream, serves live JSON and the dashboard over HTTP
- **Dashboard** — real-time gauges, feature-history scope, live radar signature plot, and escalating Normal / Warning / Critical states
- Accessible on a phone over local WiFi

## Features

- **Manual mode** — enter motor HP; thresholds are set automatically from NEC full-load-current tables
- **Learn mode** — baselines a healthy motor for a set duration (up to 10 minutes), then sets thresholds statistically: mean + 3σ for warning, mean + 5σ for trip
- **Priority-ordered alarms** — vibration > temperature > current > acoustic (acoustic trusted least, as it is noise-prone)
- **CSV export** for logging and offline analysis
- **Sensor-range awareness** — warns if the entered motor size exceeds the current clamp's range

## Engineering challenges solved

- Correct RMS via sum-of-squares rather than peak detection
- FPU-enable requirement for float math on bare-metal (silent HardFault otherwise)
- Proper C-runtime startup, which fixed a debugger visibility issue
- DS18B20 1-Wire timing and the mandatory pull-up
- I2C bus debugging with per-stage fault diagnostics
- Analog/digital ground separation to eliminate cross-sensor noise

## Scope notes

- The "learning" is statistical baseline detection (mean + kσ), not a trained ML model. It is best described as adaptive statistical anomaly detection.
- Current and temperature limits are grounded in standards. Vibration and acoustic thresholds are placeholders meant to be baselined on a real motor.
- Assembled on a breadboard. Perfboard or a soldered build is recommended for deployment stability.

## Repository structure
