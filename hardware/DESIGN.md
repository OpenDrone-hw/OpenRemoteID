# OpenRemoteID — Hardware Design Document

## Overview
Open-source FAA + EU compliant Remote ID broadcast module for drones.
ESP32-C3-MINI-1 (pre-certified FCC/CE) + ATGM336H-5NR32 GPS + U.FL antenna connector.
2-layer PCB, all 0402 passives, JLCPCB assembly.

## Compliance
- **US:** 14 CFR Part 89, ASTM F3411-22a
- **EU:** EU 2019/945 + 2022/851, EN 4709-002
- Barometric altitude NOT required by FAA (geometric altitude only, 14 CFR 89.320)
- Broadcasts on all four ASTM F3411 transport protocols simultaneously

## Target Specs
| Spec | Value |
|------|-------|
| Size | ~17×24mm |
| Weight | <4g (excl. antenna puck) |
| Power input | 5V (from FC BEC) |
| Current | ~80mA typical, ~360mA peak (WiFi TX) |
| Broadcast | BLE 4 Legacy + BLE 5 Long Range + WiFi Beacon + WiFi NaN |
| GPS | ATGM336H-5NR32 (GPS+BDS, AT6558R, built-in SAW+LNA+TCXO) |
| GPS sensitivity | -148 dBm acquisition, -162 dBm tracking |
| GPS accuracy | 2.5m CEP50 |
| GPS TTFF | 32s cold, 1s hot (with VBAT backup) |
| GPS antenna | External via U.FL/IPEX connector |
| Certification | FCC/CE/IC via ESP32-C3-MINI-1 modular cert |
| Passives | All 0402 |
| License | CERN-OHL-S-2.0 |

## BOM — Final

| Ref | Part | MPN | LCSC | Package | Qty | Unit Cost |
|-----|------|-----|------|---------|-----|-----------|
| U1 | WiFi+BLE module | ESP32-C3-MINI-1-N4 | C2838502 | 13.2×16.6×2.4mm | 1 | $2.01 |
| U2 | GPS receiver | ATGM336H-5NR32 | C5117921 | 10.1×9.7×2.4mm LCC-18 | 1 | $1.52 |
| U3 | 3.3V LDO 500mA | ME6211C33M5G-N | C82942 | SOT-23-5 | 1 | $0.04 |
| D1 | Status LED green | 16-213/GHC-YR1S1/3T | C74338 | 0402 | 1 | $0.02 |
| D2-D4 | TVS 5V | PESD0402V05 | C19626254 | 0402 | 3 | $0.006 |
| SW1 | Boot/config button | B3U-1000P(M) | Omron | 2.5×3×0.7mm | 1 | $0.15 |
| J1 | GPS antenna connector | CONUFL001-SMD-T | C2685037 | U.FL 2.6×2.6mm | 1 | $0.05 |
| C1 | LDO input bulk | 10µF X5R 10V | basic | 0402 | 1 | $0.01 |
| C2 | LDO output bulk | 22µF X5R 6.3V | basic | 0402 | 1 | $0.02 |
| C3 | Module VCC decouple | 100nF X7R 16V | basic | 0402 | 1 | $0.005 |
| C4 | GPS VCC decouple | 100nF X7R 16V | basic | 0402 | 1 | $0.005 |
| C5 | EN RC filter | 1µF X7R 10V | basic | 0402 | 1 | $0.005 |
| R1 | EN pull-up | 10k | basic | 0402 | 1 | $0.003 |
| R2 | LED series resistor | 1k | basic | 0402 | 1 | $0.003 |
| | | | | **17 placements** | **17** | **$3.90** |

### Why These Parts

**ESP32-C3-MINI-1-N4** — Pre-certified FCC/CE/IC module. Eliminates: 40MHz crystal,
load caps, RF matching, PCB trace antenna, and FCC testing ($10-30K). Built-in 4MB flash,
PCB antenna, all internal decoupling. $2.01 for a complete radio solution.

**ATGM336H-5NR32** — AT6558R GNSS SoC. Built-in SAW filter + LNA + TCXO = zero external
RF components between antenna connector and module. GPS+BDS dual constellation.
-162 dBm tracking. $1.52. Same 10.1×9.7mm LCC-18 footprint as Quectel L76K (drop-in upgrade path).

**ME6211C33M5G-N** — 500mA 3.3V LDO in SOT-23-5. ESP32-C3 peaks at 335mA during WiFi TX,
ATGM336H draws 26mA. Total peak ~365mA. 500mA gives headroom. $0.04.

**PESD0402V05** — 0402 TVS diodes, one per external pad (5V, RX, TX). Smaller total area
and cheaper than a SOT-23-6 multi-channel part. $0.006 each.

**B3U-1000P** — Omron 2.5×3×0.7mm tactile switch. Same part as OpenFC. Needed for boot
mode entry and WiFi config mode activation. Low profile.

**CONUFL001-SMD-T** — U.FL/IPEX GPS antenna connector. Same as OpenFC ELRS antenna
connector. User connects a standard GPS antenna puck ($2, widely available). Transfers
directly to OpenFC Pro. Module can be stuffed inside frame; antenna puck on top for sky view.

**No barometer** — FAA 14 CFR 89.320 requires geometric altitude only. ASTM F3411 accepts
AltitudeBaro = "unknown" (INV_ALT = -1000). No commercial standalone RID module has a baro.

**No crystal** — Built into ESP32-C3-MINI-1 module.

**No external EEPROM** — ESP32 NVS flash stores operator ID, serial number, config.

**No RTC** — GPS provides UTC time.

## Schematic

### Power
```
J_5V pad ──► D2 (TVS to GND)
         ──► C1 (10µF) ──► U3 pin 1 VIN (ME6211)
                            U3 pin 3 VOUT ──► +3.3V
                            U3 pin 2 GND ──► GND
                            U3 pin 4 CE ──► VIN (always enabled)
                            U3 pin 5 NC
+3.3V ──► C2 (22µF)
+3.3V ──► U1.VCC, U2.VCC, U2.VBAT
```

### ESP32-C3-MINI-1-N4 (U1)
Module pinout (top view, pin 1 bottom-left):
```
Pin  Name    Connection
1    GND     GND
2    3V3     +3.3V + C3 (100nF)
3    EN      R1 (10k to 3.3V) + C5 (1µF to GND)
4    IO0     NC
5    IO1     NC
6    IO2     NC
7    IO4     U2 pin 2 TXD (GPS NMEA output → ESP RX)
8    IO5     U2 pin 3 RXD (ESP TX → GPS config input)
9    IO6     NC
10   IO7     NC
11   IO8     R2 (1k) → D1 anode (LED, cathode to GND)
12   IO9     SW1 (to GND, internal pull-up)
13   IO10    NC (internal flash, do not use)
14   NC      NC
15   GND     GND
16   IO20    J_RX pad → D3 (TVS) — UART0 RX from FC (MSP)
17   IO21    J_TX pad → D4 (TVS) — UART0 TX to FC
18   IO18    NC
19   IO3     NC
20   IO19    NC
21   RXD0    NC (directly bonded to IO20 internally)
22   TXD0    NC (directly bonded to IO21 internally)
```

### ATGM336H-5NR32 (U2)
LCC-18 pinout (top view, from datasheet page 7):
```
Pin  Name      Connection
1    GND       GND
2    TXD       U1 pin 7 IO4 (ESP UART1 RX)
3    RXD       U1 pin 8 IO5 (ESP UART1 TX)
4    1PPS      NC (route to test pad if space)
5    ON/OFF    +3.3V (high = active)
6    VBAT      +3.3V (backup for RTC/SRAM, enables 1s hot start)
7    NC        NC
8    VCC       +3.3V + C4 (100nF)
9    nRESET    float (internal pull-up)
10   GND       GND
11   RF_IN     J1 U.FL connector center pin (50Ω)
12   GND       GND
13   NC        NC
14   VCC_RF    NC (3.3V output for active antenna — unused with passive)
15   Reserved  float
16   SDA       float
17   SCL       float
18   Reserved  float
```

### External Pads
```
J_5V   ── 5V power input, protected by D2 (TVS)
J_GND  ── Ground
J_RX   ── ESP32 IO20 (UART0 RX), protected by D3 (TVS)
           Receives MSP GPS data from FC. Optional.
J_TX   ── ESP32 IO21 (UART0 TX), protected by D4 (TVS)
           Sends RID status to FC. Optional.
```

Castellated pads, 1.27mm pitch, one edge of PCB.

### User Interface
- **SW1 (B3U-1000P):** Hold during power-on → boot mode for firmware flash.
  Short press during operation → toggle WiFi AP config mode.
- **D1 (green LED):** Off=no power, slow blink=GPS acquiring,
  fast blink=broadcasting, solid=error.
- **J1 (U.FL):** Connect GPS antenna puck. Must have sky view.

## PCB Layout

### Board size: ~17×24mm, 2-layer, 1.6mm FR4
```
      17mm
  ┌────────────────┐
  │ J1 (U.FL)      │ ← GPS antenna connector, top edge
  │                │
  │ ┌────────────┐ │
  │ │ ATGM336H   │ │ ← GPS module 10.1×9.7mm
  │ │  5NR32     │ │
  │ └────────────┘ │
  │ C4  R1  C5     │ ← passives
  │ ┌────────────┐ │
  │ │ ESP32-C3   │ │ ← WiFi/BLE module 13.2×16.6mm
  │ │ MINI-1-N4  │ │    PCB antenna at module bottom
  │ │            │ │
  │ └────────────┘ │
  │ U3 D2 D3 D4   │ ← LDO + TVS
  │ SW1 C1 C2 D1  │ ← button, caps, LED
  │ R2             │
  │ 5V GND RX TX   │ ← castellated pads, bottom edge
  └────────────────┘
        24mm
```

### Layer stackup
- **Top:** All components, signal traces, U.FL feed
- **Bottom:** Continuous ground plane

### Layout rules
1. U.FL connector at top edge. 50Ω trace from J1 to U2 RF_IN (pin 11). Keep short, no vias.
2. Ground plane on bottom layer — continuous, no splits. Critical for GPS + BLE performance.
3. ESP32-C3-MINI-1 oriented with its PCB antenna toward bottom edge (opposite from GPS).
4. ≥5mm between GPS RF_IN area and ESP32 module antenna area.
5. ME6211 LDO: C1 (input) and C2 (output) within 3mm of LDO pins.
6. ATGM336H: C4 within 2mm of VCC pin (pin 8).
7. All GND pins stitched to bottom plane via nearby vias.
8. GPS RF_IN trace: controlled impedance 50Ω, ground-backed on bottom layer.

## Firmware

### Architecture
```
OpenRemoteID firmware (custom, based on opendroneid-core-c)
├── GPS driver
│   ├── NMEA parser on UART1 (IO4/IO5 → ATGM336H)
│   └── Extracts: lat, lon, alt, speed, heading, time, sat count
├── FC interface (optional)
│   └── MSP parser on UART0 (IO20/IO21 → FC)
│       Receives GPS data from Betaflight if connected
├── Position manager
│   ├── Selects best GPS source (FC or onboard)
│   ├── Records first fix as operator/takeoff position
│   └── Populates ODID_UAS_Data structure
├── Broadcast engine
│   ├── opendroneid-core-c message encoding (ASTM F3411-22a)
│   ├── BLE 4 Legacy Advertising
│   ├── BLE 5 Long Range (Coded PHY)
│   ├── WiFi Beacon
│   └── WiFi NaN
├── Configuration
│   ├── ESP32 NVS parameter storage
│   ├── WiFi AP web interface (operator ID, UA serial number, region)
│   └── PCAS GPS config commands (baud rate, constellation, update rate)
└── Status
    └── LED driver (GPIO8)
```

### Critical firmware note
ArduRemoteID does NOT support standalone GPS (no NMEA parser, no standalone mode).
It only receives pre-computed data via MAVLink/DroneCAN from a flight controller.

Options:
1. **Fork ArduRemoteID** — add NMEA parser + ODID message construction. The broadcast
   engine and opendroneid-core-c encoding are reusable. ~5-8 days work for NMEA + MSP.
2. **Write from scratch** — use opendroneid-core-c library directly on ESP-IDF.
   More work but cleaner architecture. No MAVLink dependency.
3. **FC-connected only** — skip standalone GPS, always require FC connection.
   ArduRemoteID works as-is with MAVLink from ArduPilot. Betaflight needs MSP fork.

**Recommendation:** Option 1. Fork ArduRemoteID, add NMEA parser for standalone mode
and MSP parser for Betaflight mode. Both use the same broadcast engine.

## Reuse for OpenFC Pro

| Component | Standalone Module | OpenFC Pro | Shared? |
|-----------|-------------------|------------|---------|
| ATGM336H-5NR32 | On module PCB | On FC PCB | Same part, same footprint |
| U.FL connector | J1 for GPS antenna | Same connector | Same part (CONUFL001-SMD-T) |
| GPS antenna puck | User-supplied | User-supplied | Same accessory |
| ESP32-C3 | MINI-1 module | Bare ESP32-C3FH4 chip | Same firmware binary |
| LDO | ME6211C33 | WL9005D4-33 (existing) | Both 3.3V/500mA |
| Firmware | Standalone + MSP | MSP only (GPS via BF) | Same codebase |
| B3U-1000P | On module | Already on OpenFC | Same part |
| CONUFL001-SMD-T | On module | Already on OpenFC | Same part |

The OpenFC Pro adds: ATGM336H-5NR32 + U.FL connector + ESP32-C3FH4 (bare chip, identical
to existing ELRS chip) to the current OpenFC design. GPS data flows: ATGM336H → RP2354B
(Betaflight, UART0) → ESP32-C3 RID (MSP via PIO UART).

## Compliance Requirements (from BlueMark audit findings)

Source: BlueMark's 2024 compliance audit of competing modules found widespread failures.
These are the requirements we MUST meet to avoid the same pitfalls.

### Mandatory Broadcast Modes
- **BLE Legacy Advertising** (BLE 4) — Non-connectable, Non-scannable type
- **BLE 5 Long Range** (Coded PHY) — Non-connectable, Non-scannable type
- **WLAN Beacon** (WiFi 2.4GHz) — vendor-specific IE (OUI FA:0B:BC, type 0x0D)
- **WiFi NAN is NOT allowed in USA** — must be disabled for US region
- All three must broadcast simultaneously at 1Hz minimum

### Output Power (ASTM F3586-22 Section 7.8.1)
- Average EIRP around horizontal plane ≥ **+3 dBm**
- Peak-to-Average gain in horizontal plane ≤ **4 dB**
- ESP32-C3-MINI-1 supports up to +21 dBm conducted. With module's ~0 dBi
  PCB antenna, we should clear +3 dBm. Must verify with antenna pattern test.

### Antenna Pattern
- Must be generally omnidirectional in horizontal plane
- **IFA (Inverted-F) antennas FAIL** — too much directional variation (5-6 dB P2A)
- ESP32-C3-MINI-1 uses a meander/PCB trace antenna. It IS FCC certified
  (2AC7Z-ESPC3MINI1) with this antenna, but ASTM F3586-22 is a separate
  requirement from FCC Part 15. Must test mounted on our PCB.
- **Risk:** If our board layout degrades the antenna pattern below spec, we may
  need to add an external chip antenna or U.FL for 2.4G BLE/WiFi as well.

### FCC ID (14 CFR 89.530(c)(4))
- Every broadcast module MUST have a valid FCC ID
- ESP32-C3-MINI-1 has FCC ID: 2AC7Z-ESPC3MINI1 ✓
- Our product uses the module's modular certification — no separate FCC testing
  needed as long as we don't modify the RF path
- Must label per 14 CFR 89.525

### Take-off Position (14 CFR 89.320(h)(3))
- Record GPS position at takeoff
- **MUST NOT change during flight** (HolyStone failed: 300m drift)
- Accuracy within 100 feet (~30m)
- Firmware must latch position once and never update

### Declaration of Compliance (14 CFR 89.510-540)
- Must submit DoC to FAA for the module to be legal for sale
- Requires independent external audit (14 CFR 89.515(b)(2))
- Module serial numbers must be registered on FAA DroneZone

### BLE Advertisement Type
- MUST be Non-connectable, Non-scannable
- Some modules use wrong advertisement type — fails Wireshark packet inspection
- Verify with OpenDroneID receiver app + Wireshark during testing

## Open Issues

1. **Firmware:** Write standalone RID firmware on PlatformIO/ESP-IDF. NMEA parser,
   opendroneid-core-c encoding, BLE Legacy + BLE 5 LR + WiFi Beacon broadcast,
   NVS config, WiFi AP web interface. Estimate: 2-3 weeks.
2. **Antenna pattern compliance:** ESP32-C3-MINI-1 PCB antenna may not meet
   ASTM F3586-22 omnidirectional requirement when mounted on our 17×24mm board.
   Needs antenna pattern measurement. Fallback: add U.FL for external 2.4G antenna.
3. **GPS cold start:** 32s is borderline. Consider A-GNSS to reduce to <10s.
4. **GPS antenna puck selection:** Recommend a specific cheap passive GPS antenna
   puck with IPEX connector as a kit accessory.
5. **JLCPCB assembly:** B3U-1000P is not on LCSC. Source via consignment or find
   LCSC equivalent.
6. **FAA Declaration of Compliance:** Requires external audit. Budget $5-10K+
   for compliance testing and DoC submission.
7. **Board thickness:** Consider 0.8mm PCB instead of 1.6mm to reduce weight.
8. **ESP32-C3-MINI-1 pin 21/22:** Verify IO20/IO21 vs RXD0/TXD0 bonding.
   Datasheet shows both exposed — must not connect both.
