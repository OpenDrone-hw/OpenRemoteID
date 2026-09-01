# OpenRemoteID

Incomplete two-layer Remote ID hardware concept using an ESP32-C3-MINI-1 radio
module and ATGM336H GNSS receiver. It has no firmware and is not a validated,
certified or released product.

## Repo

| | |
| --- | --- |
| Designed in | KiCad 10 |
| Project | `hardware/OpenRemoteID.kicad_pro` |
| Schematic | `hardware/OpenRemoteID.kicad_sch` |
| Board | `hardware/OpenRemoteID.kicad_pcb`, 2 copper layers, 1.6 mm |
| Local library | `hardware/lib.kicad_sym`, `hardware/lib.pretty/`, `hardware/lib.3dshapes/` |
| Shared library | `hardware/KiCad-Library/`, pinned submodule; exact component datasheets resolve through `OPENDRONE_LIB` |
| Design boundary | `hardware/DESIGN.md` |
| License | CERN-OHL-S-2.0 |

## Implemented state

The schematic and PCB contain six placed devices: ESP32-C3-MINI-1-N4 (`U2`),
ATGM336H-5NR-32 (`U3`), ME6211C33M5G-N (`LDO2`), U.FL (`RF2`), switch (`SW2`)
and LED (`LED2`). The PCB has no tracks, vias or copper zones. KiCad 10 ERC
reports 85 errors and one warning. Treat all other architecture, pin mapping,
dimensions, performance and compliance language as intent until the design or
test evidence proves it.

## Intended architecture

The intended power path is 5 V input to a 3.3 V LDO. The GNSS receiver supplies
position and time to the ESP32-C3; the radio is intended to broadcast Remote ID.
External intent is 5 V, ground, UART RX/TX and a passive GNSS antenna on U.FL.
No firmware source or executable interface contract is checked in.

## Working rules

- Use the KiCad files as the hardware authority and `hardware/DESIGN.md` only as
  a statement of current boundary and intent.
- Do not claim certification, compliance, approval, current draw, RF range,
  board size or BOM cost without product-level evidence in this repository.
- Use KiCad-aware tools for circuit or layout changes; do not blind-edit KiCad
  files as text.
- Keep research as sourced reference material. A competitor claim or component
  datasheet does not establish product behaviour.
- Do not add task lists or decisions for future agents. Record verified design
  state and validation results.

## Verification

```sh
kicad-cli sch erc hardware/OpenRemoteID.kicad_sch
kicad-cli pcb drc --schematic-parity hardware/OpenRemoteID.kicad_pcb
git diff --check
```

Report exact ERC and DRC results. Findings only become release-approved through
the reviewed limits in the OpenDrone
[release standard](https://github.com/OpenDrone-hw/.github/blob/main/RELEASES.md);
new types and increased counts still block release preparation. Reusable release
automation comes from Incutec hardware tooling.
