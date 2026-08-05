# OpenRemoteID

Open-source Remote ID broadcast module for drones. FAA + EU compliant.

Status: schematic and component selection complete, PCB layout not routed yet, no firmware yet.

## Features

### Wireless
- **ESP32-C3-MINI-1**: BLE 4/5 + WiFi, FCC/CE/IC pre-certified (2AC7Z-ESPC3MINI1)
- Broadcasts BLE 4 Legacy + BLE 5 Long Range + WiFi Beacon simultaneously
- ASTM F3411-22a / EN 4709-002 compliant message encoding via opendroneid-core-c

### GPS
- **ATGM336H-5NR32**: GPS + BeiDou, AT6558R chipset
- Built-in SAW filter, LNA, TCXO: no external RF components needed
- 2.5m accuracy, 32s cold start, -162 dBm tracking sensitivity
- External GPS antenna via U.FL/IPEX connector

### Interface
- **5V** power input (from FC BEC or PDB)
- **UART** GPS passthrough to flight controller (NMEA relay for Betaflight GPS Rescue/OSD)
- **WiFi AP** configuration mode (operator ID, serial number, region)
- **Status LED** + **boot/config button**
- Castellated solder pads (4 pads: 5V, GND, RX, TX)

### Target specs
| Spec | Value |
|------|-------|
| Board size | ~13.4x23.8mm, 2-layer |
| Weight | <4g (excl. antenna puck) |
| BOM cost | ~$3.90 (17 components) |
| Power | 5V input, ~80mA typical |
| Passives | All 0402 |
| Assembly | JLCPCB, LCSC parts |

## How It Works

The module is **fully standalone**: it has its own GPS, its own BLE/WiFi radio, and its own processor. Just wire 5V + GND from the drone. No flight controller integration needed for Remote ID compliance.

**Optional GPS passthrough:** Wire the module's TX pad to an FC UART RX and the module relays NMEA data from its GPS to Betaflight/iNAV for GPS Rescue and OSD coordinates. The FC gets a GPS source for free.

**Configuration:** Hold the boot button during power-on to enter WiFi AP mode. Connect with any phone/laptop browser to set operator ID, serial number, and region.

## Repository Structure

```
OpenRemoteID/
├── README.md
├── hardware/
│   ├── DESIGN.md            ← Full design document (netlist, BOM, layout, compliance)
│   ├── OpenRemoteID.kicad_pro
│   ├── OpenRemoteID.kicad_sch
│   ├── OpenRemoteID.kicad_pcb
│   ├── lib.kicad_sym        ← Local symbol library (16 symbols)
│   ├── lib.pretty/          ← Local footprint library (17 footprints)
│   ├── lib.3dshapes/        ← 3D models (STEP + WRL)
│   └── datasheets/          ← IC datasheets (local copies)
└── research/                ← Remote ID module market research
```

All libraries are project-local. No external library setup required.

## Compliance

- **US:** 14 CFR Part 89, ASTM F3411-22a, ASTM F3586-22
- **EU:** EU 2019/945 + 2022/851, EN 4709-002
- FCC certification via ESP32-C3-MINI-1 modular approval
- FAA Declaration of Compliance required before commercial sale

## Firmware

Custom standalone firmware, not started yet. Planned stack:
- [opendroneid-core-c](https://github.com/opendroneid/opendroneid-core-c) for ASTM F3411-22a message encoding
- ESP-IDF / PlatformIO build system
- NMEA parser for direct GPS input from ATGM336H
- BLE + WiFi broadcast engine
- NVS parameter storage, WiFi AP web configuration

No existing open-source RID firmware supports standalone GPS operation: ArduRemoteID only accepts MAVLink/DroneCAN from a flight controller. This project needs its own firmware for standalone use.

## Part of OpenDrone

This module is part of the [OpenDrone](https://github.com/incutec-hw) open-source drone electronics ecosystem by [Incutec](https://github.com/incutec-hw). Designed to work standalone with any drone, or integrated into the OpenFC Pro flight controller.

## License

Hardware: [CERN-OHL-S-2.0](https://ohwr.org/cern_ohl_s_v2.txt)
Firmware: MIT (planned)
