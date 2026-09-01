# OpenRemoteID

Open hardware for a standalone broadcast Remote ID module built around an
ESP32-C3-MINI-1 radio module and an ATGM336H GNSS receiver.

## Status

This repository is an incomplete hardware concept, not a compliant or released
product. The KiCad schematic contains six placed devices and currently reports
85 ERC errors. The two-layer PCB contains the same six footprints and no routed
tracks, vias or copper zones. No firmware is present.

The intended interfaces are 5 V power, ground, UART RX/TX, a GNSS antenna on
U.FL, a status LED and a push button. See [hardware/DESIGN.md](hardware/DESIGN.md)
for the boundary between checked-in design facts and design intent.

## Repository

- `hardware/OpenRemoteID.kicad_sch`: incomplete schematic
- `hardware/OpenRemoteID.kicad_pcb`: incomplete two-layer placement
- `hardware/lib.kicad_sym`, `hardware/lib.pretty/`, `hardware/lib.3dshapes/`:
  project-local libraries
- `hardware/datasheets/`: component datasheets
- `research/`: market research; it is reference material, not product evidence

## Regulatory position

ASTM F3411 and EN 4709-002 are design targets only. This repository contains no
completed firmware, conformity assessment, declaration, radio test report or
authority acceptance for this product. Certification or modular approval of a
component does not by itself certify the finished product.

## License

Hardware is licensed under [CERN-OHL-S-2.0](LICENSE).
