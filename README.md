# OpenRemoteID

Standalone Remote ID broadcast module for drones, FAA and EU compliant. Its
own GPS, its own BLE and WiFi radio, its own processor: wire 5 V and ground
from the drone and it broadcasts. An optional UART relays the GPS to the
flight controller so Betaflight gets a position for free. A schematic and part
selection exist in `hardware/`; the layout is not routed and there is no
firmware. The full design reference is [hardware/DESIGN.md](hardware/DESIGN.md).

[![Status](https://img.shields.io/endpoint?url=https://opendrone.be/api/status/OpenRemoteID.json)](https://github.com/OpenDrone-hw/.github/blob/main/CONTRIBUTING.md#the-life-of-a-project)
[![Discord](https://img.shields.io/badge/Discord-join-5865F2?logo=discord&logoColor=white)](https://discord.gg/v3sWmTcx3R)

Nobody holds this board yet: claim it on Discord.

## Why

Remote ID is mandatory for most flying in the US and the EU, and the modules
sold for it are closed, overpriced for what is a radio and a GPS, and often
non-compliant: BlueMark's 2024 audit found wrong BLE advertisement types,
drifting take-off positions and antenna patterns out of spec. An open module
built on a pre-certified radio, with the compliance requirements written down
next to the schematic, fixes both the price and the trust problem. The same
parts and firmware then drop into a future OpenFC with Remote ID on board.

## Specifications

| | |
|---|---|
| Radio | ESP32-C3-MINI-1-N4, FCC/CE/IC modular certification |
| Broadcast | BLE 4 Legacy + BLE 5 Long Range + WiFi Beacon, simultaneous |
| Standards | ASTM F3411-22a, ASTM F3586-22, EN 4709-002 |
| GPS | ATGM336H-5NR32, GPS + BeiDou, external antenna on U.FL |
| GPS performance | 2.5 m CEP50, 32 s cold start, -162 dBm tracking |
| Power | 5 V in, 80 mA typical, 360 mA peak |
| Interface | 4 castellated pads: 5V, GND, RX, TX |
| Configuration | WiFi AP web page, boot button to enter |
| Size | 13.4 x 23.8 mm, 2 layer |
| Weight | under 4 g without antenna |
| Parts | 17 placements, all 0402 passives, about 3.90 USD |

## Constraints

- No RF design of our own: the radio is a pre-certified module and its RF path
  is not modified, so the FCC ID (2AC7Z-ESPC3MINI1) carries over. Everything
  outside the module is DC and digital.
- Broadcast rules from ASTM F3411 and F3586: all three transports at 1 Hz or
  more, non-connectable non-scannable BLE advertisements, WiFi NAN off in the
  US, average EIRP at the horizon at least +3 dBm with no more than 4 dB
  peak-to-average.
- Take-off position is latched once and never updated in flight (14 CFR
  89.320(h)(3)).
- Standalone first: must work with nothing but 5 V and ground. FC integration
  is optional and over UART.
- JLCPCB assembly from LCSC parts, 0402 passives, no external EEPROM or crystal.
- Selling it in the US needs an FAA Declaration of Compliance with an external
  audit; in the EU, EN 4709-002 under 2019/945.

## Prior art

- [research/RemoteID_Modules_Research.md](research/RemoteID_Modules_Research.md):
  the market of standalone, FC-connected and FPV inline modules, plus open
  firmware projects.
- [ArduRemoteID](https://github.com/ArduPilot/ArduRemoteID): open broadcast
  engine, but FC-fed only (MAVLink, DroneCAN); no standalone GPS mode.
- [opendroneid-core-c](https://github.com/opendroneid/opendroneid-core-c):
  the reference F3411 message encoder.
- [hardware/DESIGN.md](hardware/DESIGN.md): part choices, schematic notes,
  layout rules, and the compliance findings distilled from BlueMark's audit.

## Open questions

- Firmware: fork ArduRemoteID and add NMEA plus MSP parsers, or write from
  scratch on opendroneid-core-c.
- Antenna pattern: does the module's PCB antenna still meet F3586 mounted on
  a 13.4 x 23.8 mm board, or does the 2.4 GHz side need its own U.FL.
- The boot button (Omron B3U-1000P) is not on LCSC: consignment or an LCSC
  equivalent.
- 0.8 mm board instead of 1.6 mm to save weight.
- Which GPS antenna puck to recommend or bundle.
- ESP32-C3-MINI-1 pins 21/22: IO20/IO21 versus RXD0/TXD0 bonding, only one
  pair may be connected.

## In the line

What pairs with what, and what is available:
[opendrone.be](https://opendrone.be).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

Hardware licensed under [CERN-OHL-S-2.0](https://ohwr.org/cern_ohl_s_v2.txt),
see [LICENSE](LICENSE). Firmware, once it exists, MIT.
