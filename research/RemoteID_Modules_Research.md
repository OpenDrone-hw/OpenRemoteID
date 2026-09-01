# Remote ID Modules & Solutions — Complete Market Research (2025-2026)

Last updated: 2026-03-26

This is a dated market snapshot, not evidence about OpenRemoteID and not a
current certification register. Verify prices, availability and regulatory
status against primary sources before using them.

---

## Table of Contents

1. [Standalone Broadcast Modules (Battery-Powered)](#standalone-broadcast-modules)
2. [FC-Integrated / OEM Modules (Needs Flight Controller)](#fc-integrated--oem-modules)
3. [FPV-Specific Modules (Inline GPS)](#fpv-specific-modules)
4. [Integrated Manufacturer Solutions (DJI etc.)](#integrated-manufacturer-solutions)
5. [Open Source Firmware Projects](#open-source-firmware-projects)
6. [Summary Comparison Table](#summary-comparison-table)

---

## Standalone Broadcast Modules

These are self-contained modules with built-in GPS and battery. Attach to any drone, power on, fly.

### 1. BlueMark DroneBeacon DB120

| Field | Detail |
|-------|--------|
| **Manufacturer** | BlueMark Innovations (Netherlands) |
| **Price** | ~$150-180 |
| **Size** | 48 x 38 x 28 mm |
| **Weight** | 25g |
| **Protocols** | Bluetooth 4/5 + WiFi 2.4 GHz Beacon |
| **Compliance** | FAA (RID000000058), EU (ASD-STAN DIN EN 4709-002), ASTM F3411-22a |
| **GPS** | Built-in GPS + GLONASS, 2.5m accuracy |
| **Interface** | Standalone (attach with 3M dual-lock or M5 screws) |
| **Power** | Internal LiPo 3.7V 600mAh, 3+ hours, USB-C charging (45-60 min) |
| **TX Power** | +20 dBm, up to 5 km detection range |
| **Open Source** | Proprietary firmware |

### 2. BlueMark DroneBeacon DB150

| Field | Detail |
|-------|--------|
| **Manufacturer** | BlueMark Innovations |
| **Price** | ~$120 (estimated) |
| **Size** | ~half the size of DB120 |
| **Weight** | 12.5g |
| **Protocols** | Bluetooth + WiFi (same as DB120) |
| **Compliance** | FAA + EU |
| **GPS** | Built-in GNSS |
| **Interface** | Standalone |
| **Power** | Internal battery, 120 min (2 hours) |
| **Open Source** | Proprietary firmware |

### 3. Dronetag Beacon V2

| Field | Detail |
|-------|--------|
| **Manufacturer** | Dronetag (Czech Republic) |
| **Price** | $149 / EUR 139 |
| **Size** | 37 x 26 x 16 mm |
| **Weight** | 17g |
| **Protocols** | Bluetooth 2.4 GHz (BT4/BT5) |
| **Compliance** | FAA, EASA (EU), CAAS (Singapore), CAA (UK) |
| **GPS** | Built-in uBlox M10 GNSS + barometer + accelerometer |
| **Interface** | Standalone (attach with adhesive/strap) |
| **Power** | Li-Po 3.7V 200mAh, 10-18 hours battery life, USB-C charging |
| **Open Source** | Proprietary firmware |

### 4. Dronetag BS

| Field | Detail |
|-------|--------|
| **Manufacturer** | Dronetag |
| **Price** | $89 |
| **Size** | Very compact |
| **Weight** | 3g (including antennas) |
| **Protocols** | Bluetooth (BT4/BT5), 3 km range |
| **Compliance** | FAA |
| **GPS** | Built-in GNSS |
| **Interface** | Standalone |
| **Power** | Internal battery |
| **Open Source** | Proprietary firmware |

### 5. Dronetag Mini

| Field | Detail |
|-------|--------|
| **Manufacturer** | Dronetag |
| **Price** | EUR 299 + subscription (EUR 15/month for Network RID) |
| **Size** | Compact |
| **Weight** | 32g |
| **Protocols** | Bluetooth (Broadcast RID) + LTE-M/NB-IoT (Network RID) |
| **Compliance** | FAA, EASA, CAAS (Singapore), CAA (UK) |
| **GPS** | Built-in GNSS |
| **Interface** | Standalone, dual-signal (Broadcast + Network RID) |
| **Power** | Internal battery, 14 hours |
| **Open Source** | Proprietary firmware |
| **Notes** | Only module with Network RID via cellular. Subscription required for NRI features. |

### 6. uAvionix pingRID

| Field | Detail |
|-------|--------|
| **Manufacturer** | uAvionix |
| **Price** | $299 |
| **Size** | 25.4 x 16.6 x 43.4 mm |
| **Weight** | 21g |
| **Protocols** | Bluetooth 4 & 5 |
| **Compliance** | FAA (ASTM F3586-22) |
| **GPS** | Built-in GPS |
| **Interface** | Standalone, no setup required |
| **Power** | Internal Li-ion 740 mWh, 2+ hours, USB-C charging |
| **Open Source** | Proprietary firmware |

### 7. Pierce Aerospace B1

| Field | Detail |
|-------|--------|
| **Manufacturer** | Pierce Aerospace |
| **Price** | ~$265-275 |
| **Size** | 74 x 24 x 19 mm |
| **Weight** | 30g |
| **Protocols** | Bluetooth + WiFi 2.4 GHz |
| **Compliance** | FAA (ASTM F3411-22), DIU Blue UAS Framework approved |
| **GPS** | Built-in GPS |
| **Interface** | Standalone (cable tie mounts) |
| **Power** | Internal LiPo, 6-8 hours, USB-C charging |
| **Open Source** | Proprietary firmware |
| **Notes** | Only RID module approved for DIU Blue UAS Framework (government/defense use). Also available as B1 Gov variant. |

### 8. Zing Z-RID Lite

| Field | Detail |
|-------|--------|
| **Manufacturer** | Zing Drone Solutions (MIT-engineered, made in California) |
| **Price** | $85 |
| **Size** | 40 x 40 x 30 mm |
| **Weight** | 30g |
| **Protocols** | Bluetooth 4 + 5 |
| **Compliance** | FAA + EASA |
| **GPS** | Built-in GNSS |
| **Interface** | Standalone |
| **Power** | Internal battery, up to 4 hours |
| **Open Source** | Proprietary |

### 9. Zing Z-RID (Original)

| Field | Detail |
|-------|--------|
| **Manufacturer** | Zing Drone Solutions |
| **Price** | $229 |
| **Size** | 50 x 35 x 25 mm |
| **Weight** | 35g |
| **Protocols** | Bluetooth + multi-band (698-960 MHz, 1710-2500 MHz) |
| **Compliance** | FAA |
| **GPS** | Built-in GNSS |
| **Interface** | Standalone |
| **Power** | 5V DC max, 0.4A max consumption |
| **Open Source** | Proprietary |

### 10. Potensic RID-916

| Field | Detail |
|-------|--------|
| **Manufacturer** | Potensic |
| **Price** | ~$30-35 |
| **Size** | Compact |
| **Weight** | <20g |
| **Protocols** | Bluetooth 5.1 (8 dBm TX, 300m+ range) |
| **Compliance** | FAA |
| **GPS** | Built-in GPS (<3m accuracy) |
| **Interface** | Standalone |
| **Power** | Internal battery, 4 hours, USB-C charging |
| **IP Rating** | IP54 |
| **Open Source** | Proprietary |

### 11. Holy Stone HSRID03

| Field | Detail |
|-------|--------|
| **Manufacturer** | Holy Stone |
| **Price** | ~$30-35 |
| **Size** | 34 x 28 x 13.5 mm |
| **Weight** | 13.5g (without Velcro) / 14.2g (with Velcro) |
| **Protocols** | Bluetooth |
| **Compliance** | FAA |
| **GPS** | Built-in GPS |
| **Interface** | Standalone |
| **Power** | Internal battery, 5 hours, USB-C charging (1.5 hrs) |
| **IP Rating** | IP54 |
| **Open Source** | Proprietary |
| **Notes** | Built-in buzzer for drone location and LED strobe lights |

### 12. Spektrum SkyID (SPMA9500)

| Field | Detail |
|-------|--------|
| **Manufacturer** | Spektrum / Horizon Hobby |
| **Price** | ~$125 (discontinued/hard to find) |
| **Size** | 34.5 x 22.5 x 18 mm |
| **Weight** | 14g |
| **Protocols** | Bluetooth 4 & 5 Long Range |
| **Compliance** | FAA (FCC certified) |
| **GPS** | Built-in GPS |
| **Interface** | Standalone or SRXL2/XBus telemetry to Spektrum receivers |
| **Power** | 3.3V - 9V input |
| **Open Source** | Proprietary |
| **Notes** | Appears discontinued. Was integrated with Spektrum telemetry ecosystem. |

### 13. Flite Test FT EZ ID

| Field | Detail |
|-------|--------|
| **Manufacturer** | Flite Test |
| **Price** | $109 |
| **Size** | 30 x 30 mm footprint, 20x20 M3 mounting holes |
| **Weight** | 10g |
| **Protocols** | Bluetooth 4 & 5 (Nordic NRF52840) |
| **Compliance** | FAA |
| **GPS** | Built-in uBlox SAM-M8Q GPS |
| **Interface** | Standalone, 2S-8S power input (10mA avg draw) |
| **Power** | Powered from drone battery (2S-8S), 10mA average |
| **Range** | Tested to 1500 ft unobstructed |
| **Open Source** | Proprietary |
| **Notes** | Cold start ~53s, warm start <20s. Companion app with "Find my plane" feature. |

---

## FC-Integrated / OEM Modules

These modules require a flight controller (ArduPilot, PX4, Betaflight, etc.) to provide GPS and flight data. They are transmit-only devices.

### 14. Holybro Remote ID Module (C3)

| Field | Detail |
|-------|--------|
| **Manufacturer** | Holybro |
| **Price** | $20-30 |
| **Size** | 38 x 26.5 x 11.5 mm (not including antenna) |
| **Weight** | 27.5g |
| **Protocols** | Bluetooth + WiFi 2.4 GHz (+20 dBm) |
| **Compliance** | FCC + CE certified (but NOT standalone FAA-approved broadcast module; requires user DoC submission) |
| **GPS** | NO built-in GPS. Requires FC with GPS via MAVLink/DroneCAN |
| **Interface** | UART (6-pin JST GH) + CAN (4-pin JST GH) to ArduPilot FC |
| **Power** | +5V from TELEM or CAN port |
| **Firmware** | ArduRemoteID (open source, GPLv2+) |
| **Chip** | ESP32-C3 |
| **Open Source** | YES - runs ArduRemoteID open source firmware |
| **Notes** | Cheapest option but requires ArduPilot FC. Standard Remote ID solution = user responsible for FAA DoC. OTA firmware update via web interface. |

### 15. CubePilot Cube ID

| Field | Detail |
|-------|--------|
| **Manufacturer** | CubePilot |
| **Price** | $39-44 |
| **Size** | 25 x 13.75 x 3.5 mm |
| **Weight** | 10g (with cable and antenna) |
| **Protocols** | Bluetooth 5.2 dual-mode (Nordic nRF52840) |
| **Compliance** | FCC + CE certified (Standard RID, user responsible for DoC) |
| **GPS** | NO built-in GPS. Requires FC to provide position data |
| **Interface** | Serial or CAN variants to ArduPilot/PX4 FC |
| **Power** | Powered from FC |
| **Open Source** | Firmware is proprietary (CubePilot) |
| **Notes** | Smallest and cheapest certified RID module. OEM-targeted. No WiFi broadcast, Bluetooth only. |

### 16. Dronetag DRI

| Field | Detail |
|-------|--------|
| **Manufacturer** | Dronetag |
| **Price** | $59 / EUR 49 |
| **Size** | 22.5 x 16 x 5 mm |
| **Weight** | 1.5g |
| **Protocols** | Bluetooth 4 & 5 (3 km range) |
| **Compliance** | FAA (ASTM F3411), EU (prEN 4709-002) |
| **GPS** | NO built-in GPS. Relies on FC position data via MAVLink |
| **Interface** | Serial (inline between FC and peripheral), compatible with Pixhawk/ArduPilot/PX4 |
| **Power** | 3.3-17V input, 3mA avg / 10mA max consumption |
| **Antenna** | U.FL port for external antenna (includes BT wire antenna) or built-in antenna variant |
| **Open Source** | Proprietary firmware |
| **Notes** | Smallest RID module on market (1.5g). OEM/integrator focused. |

### 17. FrSky FrID

| Field | Detail |
|-------|--------|
| **Manufacturer** | FrSky |
| **Price** | ~$50-70 (estimated) |
| **Size** | 36 x 20 mm |
| **Weight** | 8g |
| **Protocols** | Bluetooth 4 & 5 (BLE) |
| **Compliance** | FAA (ASTM F3586-22), FCC certified |
| **GPS** | Built-in uBlox MAX-7Q GPS (chip antenna) |
| **Interface** | FBUS/S.Port to FrSky receivers (telemetry data readable on radio) |
| **Power** | DC 4-10V |
| **Open Source** | Proprietary firmware |
| **Notes** | Integrates with FrSky telemetry ecosystem. Has own GPS but connects to FrSky RX. |

### 18. Lumenier RID

| Field | Detail |
|-------|--------|
| **Manufacturer** | Lumenier / GetFPV |
| **Price** | $13-26 |
| **Size** | Compact (30x30-ish form factor) |
| **Weight** | 9g |
| **Protocols** | Bluetooth 4 & 5 |
| **Compliance** | FAA |
| **GPS** | Built-in uBlox SAM-M10Q GPS + magnetometer |
| **Interface** | Inline between GPS and FC. GPS/mag data shared with FC for autopilot/OSD |
| **Power** | 5-34V (2S-8S) |
| **Open Source** | Proprietary firmware |
| **NDAA** | NDAA compliant |
| **Notes** | Cheapest GPS-equipped RID module. GPS/mag passthrough to FC is a strong feature. Individually tested with included test report. |

---

## FPV-Specific Modules

Designed specifically for FPV builds with inline GPS passthrough and compact stack-compatible form factors.

### 19. Phoenix UAS mRID

| Field | Detail |
|-------|--------|
| **Manufacturer** | Phoenix UAS |
| **Price** | ~$69 |
| **Size** | 24 x 14 x 8 mm |
| **Weight** | 2.2g |
| **Protocols** | Bluetooth 5 LE / BT4 |
| **Compliance** | FAA (DoC# RID000000679) |
| **GPS** | NO built-in GPS. Connects inline between M10 GPS module and FC |
| **Interface** | Inline GPS passthrough (GPS data to FC preserved for RTH/GPS rescue/OSD) |
| **Power** | 3.3-5V (1S battery or USB), <40mA |
| **LEDs** | 4 LEDs: Power, GPS Lock, Telemetry, Failure |
| **Open Source** | Proprietary firmware |
| **Notes** | Purpose-built for FPV. Extremely light. Preserves FC GPS functionality. |

### 20. BlueMark DB152fpv

| Field | Detail |
|-------|--------|
| **Manufacturer** | BlueMark Innovations |
| **Price** | ~EUR 59 |
| **Size** | 27 x 27 mm (20x20 M3 mounting holes) |
| **Weight** | 2.9g (including antenna) |
| **Protocols** | Bluetooth + WiFi |
| **Compliance** | FAA + EU |
| **GPS** | NO built-in GPS. Requires external GNSS (NMEA or UBX). Relays GPS data to FC via GPS OUT connector |
| **Interface** | 6-pin JST SH 1mm connectors, 20x20 stack compatible |
| **Power** | 4.75-15V via GPS OUT VCC pin |
| **Open Source** | Proprietary firmware |

### 21. BlueMark DB153fpv

| Field | Detail |
|-------|--------|
| **Manufacturer** | BlueMark Innovations |
| **Price** | ~EUR 59 |
| **Size** | 19 x 14 mm |
| **Weight** | 2g (including antenna) |
| **Protocols** | Bluetooth + WiFi |
| **Compliance** | FAA + EU |
| **GPS** | NO built-in GPS. Requires external GNSS. Relays GPS data to FC |
| **Interface** | Solder pads on 1.27mm grid |
| **Power** | 4.75-15V |
| **Open Source** | Proprietary firmware |
| **Notes** | Tiniest FPV RID module. Solder-pad only, no connectors. |

### 22. BlueMark DB121 / DB121pcb

| Field | Detail |
|-------|--------|
| **Manufacturer** | BlueMark Innovations |
| **Price** | ~$80-100 |
| **Size** | 36 x 38 x 28 mm (DB121) / smaller PCB-only (DB121pcb) |
| **Weight** | 11g (DB121) / 5g (DB121pcb) |
| **Protocols** | Bluetooth + WiFi |
| **Compliance** | FAA + EU |
| **GPS** | Built-in GNSS |
| **Interface** | Drone-powered (5-14V), no internal battery |
| **Power** | 5-14V from drone |
| **TX Power** | +20 dBm, up to 5 km detection range |
| **Open Source** | Proprietary firmware |
| **Notes** | Essentially a DB120 without battery. Good for permanent installations. |

---

## Integrated Manufacturer Solutions

### 23. DJI Integrated Remote ID

| Field | Detail |
|-------|--------|
| **Manufacturer** | DJI |
| **Price** | Free (firmware update) |
| **Protocols** | WiFi Aware (WiFi NaN), 1+ km range |
| **Compliance** | FAA |
| **GPS** | Uses drone's built-in GPS |
| **Interface** | Built into drone firmware |
| **Notes** | Not a separate module. DJI implements RID via firmware updates on supported models. |

**Supported DJI Models (via firmware update):**
- DJI Mini 2, Mini 3 Pro, Mini 4 Pro
- DJI Air 2S, Air 3
- DJI Mavic 3 / 3 Cine / 3 Pro
- DJI Matrice 300 RTK, Matrice 30/30T
- DJI AGRAS T30, T10
- Most DJI drones manufactured from 2022 onward

### 24. Other Integrated Solutions

Most major drone manufacturers (Autel, Skydio, Parrot) now include Remote ID in firmware on current-generation products. These are not separate modules.

---

## Open Source Firmware Projects

### 25. ArduRemoteID (ArduPilot)

| Field | Detail |
|-------|--------|
| **Repository** | https://github.com/ArduPilot/ArduRemoteID |
| **License** | GPLv2+ |
| **Supported Chips** | ESP32-S3, ESP32-C3 |
| **Protocols** | BT4 Legacy Advertising, BT5 Long Range, WiFi Beacon, WiFi NaN |
| **FC Communication** | MAVLink (serial) + DroneCAN |
| **Supported Boards** | ESP32-S3 dev board, ESP32-C3 dev board, Holybro Remote ID Module, BlueMark DB110/DB200/DB201/DB202mav/DB210pro |
| **Standards** | ASTM F3586-22 (FAA MOC), EU compatible |
| **Notes** | The primary open source RID transmitter firmware. Pre-built binaries available. OTA update support. This is what the Holybro module runs. |

### 26. OpenDroneID Core C Library

| Field | Detail |
|-------|--------|
| **Repository** | https://github.com/opendroneid/opendroneid-core-c |
| **License** | Apache 2.0 (library itself) |
| **Purpose** | Core encoding/decoding library for ODID messages |
| **Protocols** | BT4, BT5, WiFi Beacon, WiFi NaN |
| **Standards** | ASTM F3411-19, ASTM F3411-22a, ASD-STAN prEN 4709-002 |
| **Supported HW** | ESP32/S3/C3, nRF52840, TI CC2640, Linux, Raspberry Pi |
| **Notes** | Foundation library used by ArduRemoteID and many other projects. Not standalone firmware — it's a library. |

### 27. sxjack/uav_electronic_ids

| Field | Detail |
|-------|--------|
| **Repository** | https://github.com/sxjack/uav_electronic_ids |
| **License** | Open source |
| **Purpose** | Arduino library for UAV electronic IDs |
| **Supported HW** | ESP32, ESP8266 |
| **Protocols** | BT4 Legacy Advertising, WiFi NaN, WiFi Beacon (simultaneous) |
| **Notes** | Early community implementation. Foundation for ArduRemoteID and other projects. |

### 28. sxjack/remote_id_bt5

| Field | Detail |
|-------|--------|
| **Repository** | https://github.com/sxjack/remote_id_bt5 |
| **License** | Open source |
| **Purpose** | BT4 & BT5 Remote ID for nRF52 processors |
| **Supported HW** | nRF52840 |
| **Protocols** | BT4, BT5 |
| **Standards** | ASTM F3411, EN 4709-002 |

### 29. PeterJBurke/esp32-c3-remote-id

| Field | Detail |
|-------|--------|
| **Repository** | https://github.com/PeterJBurke/esp32-c3-remote-id |
| **License** | Open source |
| **Purpose** | ESP32-C3 RID implementation with monitoring tools |
| **Supported HW** | ESP32-C3 Mini 1 dev board |
| **Standards** | ASTM F3411-19 |
| **Notes** | Fork of uav_electronic_ids with ESP32-C3 specific features and Python analysis scripts. |

### 30. DIY ESP32 Build (Hackster.io / Tea and Tech Time)

Several community guides exist for building your own RID transmitter on generic ESP32-S3 or ESP32-C3 dev boards (~$5-10 hardware cost) using ArduRemoteID firmware. Requires a flight controller running ArduPilot for GPS data.

---

## Summary Comparison Table

| # | Module | Price | Weight | GPS | Protocols | Compliance | Interface | Open Source |
|---|--------|-------|--------|-----|-----------|------------|-----------|-------------|
| 1 | BlueMark DB120 | ~$160 | 25g | Yes | BT4/5 + WiFi | FAA + EU | Standalone | No |
| 2 | BlueMark DB150 | ~$120 | 12.5g | Yes | BT4/5 + WiFi | FAA + EU | Standalone | No |
| 3 | Dronetag Beacon V2 | $149 | 17g | Yes | BT4/5 | FAA+EU+UK+SG | Standalone | No |
| 4 | Dronetag BS | $89 | 3g | Yes | BT4/5 | FAA | Standalone | No |
| 5 | Dronetag Mini | EUR 299 | 32g | Yes | BT + LTE (NRI) | FAA+EU+UK+SG | Standalone | No |
| 6 | uAvionix pingRID | $299 | 21g | Yes | BT4/5 | FAA | Standalone | No |
| 7 | Pierce B1 | ~$270 | 30g | Yes | BT + WiFi | FAA + Blue UAS | Standalone | No |
| 8 | Zing Z-RID Lite | $85 | 30g | Yes | BT4/5 | FAA + EASA | Standalone | No |
| 9 | Potensic RID-916 | ~$32 | <20g | Yes | BT5.1 | FAA | Standalone | No |
| 10 | Holy Stone HSRID03 | ~$32 | 14g | Yes | BT | FAA | Standalone | No |
| 11 | Spektrum SkyID | ~$125 | 14g | Yes | BT4/5 LR | FAA | Standalone/SRXL2 | No |
| 12 | Flite Test EZ ID | $109 | 10g | Yes | BT4/5 | FAA | Standalone (2S-8S) | No |
| 13 | Holybro RID (C3) | ~$25 | 27.5g | **No** | BT + WiFi | FCC/CE (needs DoC) | UART/CAN to FC | **Yes** (ArduRemoteID) |
| 14 | CubePilot Cube ID | ~$40 | 10g | **No** | BT5.2 | FCC/CE (needs DoC) | Serial/CAN to FC | No |
| 15 | Dronetag DRI | $59 | 1.5g | **No** | BT4/5 | FAA + EU | Serial to FC | No |
| 16 | FrSky FrID | ~$60 | 8g | Yes | BT4/5 | FAA | FBUS/S.Port | No |
| 17 | Lumenier RID | ~$20 | 9g | Yes | BT4/5 | FAA | Inline GPS | No |
| 18 | Phoenix UAS mRID | ~$69 | 2.2g | **No** | BT4/5 | FAA | Inline GPS | No |
| 19 | BlueMark DB152fpv | ~EUR 59 | 2.9g | **No** | BT + WiFi | FAA + EU | 20x20 stack | No |
| 20 | BlueMark DB153fpv | ~EUR 59 | 2g | **No** | BT + WiFi | FAA + EU | Solder pads | No |
| 21 | BlueMark DB121 | ~$90 | 11g/5g | Yes | BT + WiFi | FAA + EU | Drone-powered | No |
| 22 | DIY ESP32-S3/C3 | ~$5-10 | ~5g | **No** | BT4/5+WiFi NaN+Beacon | Needs DoC | UART/CAN to FC | **Yes** (ArduRemoteID) |

---

## Key Observations

### Best Value Standalone
- **Potensic RID-916** and **Holy Stone HSRID03** at ~$30-35 are the cheapest standalone options with built-in GPS and battery. BT-only, FAA-only compliance.

### Best for FPV
- **Phoenix UAS mRID** (2.2g, $69) and **BlueMark DB153fpv** (2g, EUR 59) are the lightest options. Both need external GPS.
- **Lumenier RID** ($20, 9g) is the best value with built-in GPS and GPS passthrough to FC.

### Best for Open Source / Custom Builds
- **Holybro Remote ID** ($25) running ArduRemoteID is the cheapest path to open source RID with BT+WiFi.
- DIY ESP32-C3/S3 dev board ($5-10) with ArduRemoteID firmware is the absolute cheapest but requires ArduPilot FC.

### Best Multi-Region Compliance
- **BlueMark DB120/DB150** and **Dronetag Beacon V2** cover both FAA and EU.
- **Dronetag Mini** covers FAA, EU, UK, and Singapore.

### Government/Defense
- **Pierce Aerospace B1** is the only Blue UAS Framework approved module.

### Modules NOT Found
- **BrainFPV**: Does not appear to make a standalone Remote ID module. Their RADIX FC may support RID via ArduPilot + external module.
- **Flywoo**: No dedicated Remote ID module found.
- **iFlight / EACHINE**: No dedicated Remote ID modules found. These manufacturers focus on FPV hardware (FCs, ESCs, frames).

### Japan
- Japan has its own RID system separate from FAA/EU standards. DJI provides firmware-based RID for Japan-market drones. Dronetag has announced plans to enter the Japanese market. Most FAA/EU modules are NOT directly compatible with Japanese RID requirements.

---

## Sources

- [FPV Freedom Coalition Remote ID Modules](https://fpvfc.org/remote-id-modules)
- [FAA Remote Identification](https://www.faa.gov/uas/getting_started/remote_id)
- [BlueMark Innovations](https://bluemark.io/remote-id-for-drones/)
- [Dronetag Products](https://www.dronetag.com/compare)
- [Holybro Remote ID Docs](https://docs.holybro.com/radio/remote-id/overview-and-spec)
- [ArduRemoteID GitHub](https://github.com/ArduPilot/ArduRemoteID)
- [OpenDroneID GitHub](https://github.com/opendroneid/opendroneid-core-c)
- [CubePilot Cube ID](https://docs.cubepilot.org/user-guides/cube-id/cube-id)
- [Pierce Aerospace](https://www.pierceaerospace.net/products/b1-remote-id-beacon)
- [Phoenix UAS](https://www.phoenixuas.us/remoteid)
- [Pilot Institute Remote ID Guide](https://pilotinstitute.com/remote-id-drone-modules/)
- [GetFPV Remote ID](https://www.getfpv.com/electronics/remote-id.html)
- [sxjack/uav_electronic_ids](https://github.com/sxjack/uav_electronic_ids)
