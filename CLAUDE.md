# OpenRemoteID — Project Instructions

## What This Is
Open-source standalone Remote ID broadcast module for drones.
ESP32-C3-MINI-1 + ATGM336H-5NR32 GPS + U.FL antenna.
Part of the OpenDrone ecosystem (Incutec). CERN-OHL-S-2.0.

## Architecture
Fully standalone — own GPS, own BLE/WiFi radio, just needs 5V power.
GPS NMEA is parsed onboard and also relayed to the FC via UART for GPS Rescue/OSD.
No flight controller integration needed for Remote ID compliance.

## Key ICs
| IC | Part | LCSC | Package | Function |
|----|------|------|---------|----------|
| U1 | ESP32-C3-MINI-1-N4 | C2838502 | 13.2x16.6mm | BLE+WiFi, FCC/CE pre-certified |
| U2 | ATGM336H-5NR32 | C5117921 | 10.1x9.7mm LCC-18 | GPS+BDS, AT6558R, built-in SAW+LNA+TCXO |
| U3 | ME6211C33M5G-N | C82942 | SOT-23-5 | 5V→3.3V LDO, 500mA |
| D2-D4 | PESD0402V05 | C19626254 | 0402 | TVS on each external pad |
| D1 | 16-213/GHC-YR1S1/3T | C74338 | 0402 | Green status LED |
| SW1 | B3U-1000P(M) | Omron (consign) | 2.5x3mm | Boot/config button |
| J1 | CONUFL001-SMD-T | C2685037 | U.FL 2.6x2.6mm | GPS antenna connector |

## Pin Mapping (ESP32-C3-MINI-1)
- UART1 (IO4 RX, IO5 TX): ATGM336H GPS module (NMEA at 9600 baud)
- UART0 (IO20 RX, IO21 TX): External pads — GPS relay to FC + optional FC input
- IO8: Status LED (green, via 1k resistor)
- IO9: Boot/config button (B3U-1000P to GND)
- EN: 10k pull-up + 1µF RC filter

## Broadcast Modes (all simultaneous, 1Hz)
- BLE 4 Legacy Advertising (Non-connectable, Non-scannable)
- BLE 5 Long Range (Coded PHY, Non-connectable, Non-scannable)
- WiFi Beacon (WLAN 2.4GHz, vendor IE OUI FA:0B:BC type 0x0D)
- WiFi NAN: NOT allowed in USA (region-locked in firmware)

## Compliance Requirements
- EIRP ≥ +3 dBm average in horizontal plane, ≤4 dB peak-to-average
- Take-off position MUST be locked at first GPS fix, never updated during flight
- FCC ID via ESP32-C3-MINI-1 modular cert (2AC7Z-ESPC3MINI1)
- FAA Declaration of Compliance required for commercial sale
- No barometer needed (FAA requires geometric altitude only)

## Design Files
- `hardware/DESIGN.md` — Complete netlist, BOM, layout strategy, compliance requirements
- `hardware/OpenRemoteID.kicad_pro` — KiCad project (KiCad 9/10)
- `hardware/lib.kicad_sym` — Local symbol library (16 symbols: 7 used + 9 reserve for OpenFC Pro)
- `hardware/lib.pretty/` — Local footprint library (17 footprints)
- `hardware/lib.3dshapes/` — 3D models (15 WRL + 15 STEP)
- `hardware/datasheets/` — All IC datasheets (local PDF copies)

## Datasheets (local)
- ESP32-C3-MINI-1_datasheet.pdf, ESP32-C3_datasheet.pdf
- ATGM336H-5NR32_datasheet.pdf, ATGM336H-5N31_datasheet.pdf
- ME6211C33_datasheet.pdf
- PESD0402V05_datasheet.pdf
- ALA931C5_datasheet.pdf (GPS antenna, not used but reference)
- WL9005D4-33_datasheet.pdf (LDO, reserve for OpenFC Pro)
- USBLC6-2SC6_datasheet.pdf (ESD, reserve)
- ATGM332D-5NR32_datasheet.pdf (GPS, reserve)

## Firmware
- Custom standalone firmware on PlatformIO / ESP-IDF (planned)
- Uses opendroneid-core-c for ASTM F3411-22a message encoding
- NMEA parser for ATGM336H on UART1
- NMEA relay to FC on UART0 (GPS passthrough)
- WiFi AP web interface for configuration (operator ID, serial number, region)
- NVS parameter storage
- ArduRemoteID is NOT usable (no standalone GPS mode, MAVLink only)

## OpenFC Pro Integration
Same ATGM336H-5NR32 + U.FL connector + ESP32-C3 (bare chip on FC).
GPS data flows: ATGM336H → RP2354B (Betaflight) → ESP32-C3 RID (NMEA relay).
Reserve symbols in library: ESP32-C3FH4, WL9005D4-33, SX0B40 crystal, etc.

## Related Projects
- OpenFC: flight controller, will integrate Remote ID in Pro version
- Incutec: company command center

## Rules
- NEVER raw-edit .kicad_sch, .kicad_pcb, .kicad_pro — use Python scripts with kicad-skip
- Libraries are project-local (lib.kicad_sym, lib.pretty/, lib.3dshapes/)
- JLCPCB assembly, LCSC parts, all 0402 passives
- Production exports in hardware/production/ — use KiCad Fabrication Toolkit
