# 🐠 Smart Aquarium

🇬🇧 English | [🇭🇷 Hrvatski](README.hr.md)

**A microcomputer system for controlling and regulating aquarium conditions**.
Course project: *Embedded Computer Systems* (UgRS), FERIT Osijek, 2026.

Authors: Luka Idžanović, Nina Sučić

An ESP32-based system that automatically regulates water temperature,
simulates a daylight cycle, feeds the fish periodically, and allows manual
control of a water circulation pump.

## Features

- 🌡️ **Temperature control**: a DS18B20 sensor is read every 3 s. Below the
  set value (28 °C), a relay switches on an H7 bulb that acts as the heater.
- 🛡️ **Noise filtering**: a `-127 °C` reading (a OneWire communication error
  caused by interference from the pump) is discarded and the relay keeps its
  previous state.
- 💡 **Sunlight cycle simulation**: a WS2812B LED strip gradually brightens
  and dims (5-minute cycle in demo mode).
- 🍽️ **Automatic feeding**: an SG90 servo motor periodically opens the food
  dispenser.
- 💧 **Manual pump control**: a push button toggles the submersible pump
  (with debounce protection).

## Components

| Component | Purpose |
|---|---|
| ESP32 NodeMCU + Expansion Board | main microcontroller |
| DS18B20 (waterproof) | temperature measurement (OneWire) |
| H7 bulb 12 V / 55 W | heater (runs on 5 V, ≈ 9.6 W) |
| 2-channel 5 V relay module (*Active LOW*) | controls heater and pump |
| 5 V DC submersible pump | water circulation |
| SG90 micro servo | food dispenser |
| WS2812B LED strip (30 LEDs) | lighting |
| Push button | manual pump control |
| 5 V / 10 A power supply + WAGO 221 | power distribution |

## Wiring (ESP32 pins)

| Pin | Component |
|---|---|
| GPIO 13 | WS2812B LED strip (data) |
| GPIO 18 | SG90 servo |
| GPIO 14 | push button (`INPUT_PULLUP`) |
| GPIO 16 | relay: pump |
| GPIO 2 | relay: bulb (heater) |
| GPIO 4 | DS18B20 (data) |

## Getting Started

1. Install [Arduino IDE](https://www.arduino.cc/en/software) and ESP32 board support.
2. In the Library Manager, install: `FastLED`, `ESP32Servo`, `OneWire`, `DallasTemperature`.
3. Open [KOD.txt](KOD.txt) (rename it to `.ino` or paste it into a new sketch),
   select the ESP32 board and upload the program.
4. The serial monitor (115200 baud) shows the status of the thermostat,
   feeder and pump.

## Video Presentation

🎬 [Watch the video presentation on Google Drive](https://drive.google.com/file/d/1V9iYCyiI1syzogd-55SNvuv7ObN_iCeJ/view?usp=drivesdk)

## Documentation

Project report: [URS26 - Idžanović,Sučić.pdf](URS26%20-%20Id%C5%BEanovi%C4%87%2CSu%C4%8Di%C4%87.pdf) (Croatian)
