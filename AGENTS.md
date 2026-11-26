# OpenRemoteID

Incomplete two-layer Remote ID hardware concept: an ESP32-C3-MINI-1 radio
module and an ATGM336H GNSS receiver. It has no firmware and is not a
validated, certified or released product. The KiCad files are the hardware
authority; `hardware/DESIGN.md` states the boundary between the checked-in
design and design intent and lists the placed devices.

## Architecture

Implemented: six placed devices, ESP32-C3-MINI-1-N4 (`U2`), ATGM336H-5NR-32
(`U3`), ME6211C33M5G-N (`LDO2`), U.FL (`RF2`), switch (`SW2`) and LED
(`LED2`). The PCB has no tracks, vias or copper zones, and ERC does not pass;
run it for the current findings.

Intended: 5 V input to a 3.3 V LDO; the GNSS receiver supplies position and
time to the ESP32-C3, which broadcasts Remote ID. External interface intent
is 5 V, ground, UART RX/TX and a passive GNSS antenna on U.FL. No firmware
source or interface contract is checked in.

Treat every other architecture, pin mapping, dimension, performance and
compliance statement as intent until the design or test evidence proves it.
Do not claim certification, compliance, approval, current draw, RF range,
board size or BOM cost without product-level evidence in this repository.
The Remote ID module research (`research/remote-id-modules.md`) is sourced reference material: a competitor claim or a component
datasheet does not establish product behaviour.

## Repo

| | |
|---|---|
| KiCad project | `hardware/OpenRemoteID.kicad_pro` |
| Root schematic | `hardware/OpenRemoteID.kicad_sch` |
| Board | `hardware/OpenRemoteID.kicad_pcb`, 2 copper layers, 1.6 mm |
| Local datasheets | Linked from `hardware/DESIGN.md` "Datasheets"; no PDFs are vendored |
| Design boundary | `hardware/DESIGN.md` |

## Rules

The shared [Board rules](https://github.com/OpenDrone-hw/hardware-template/blob/main/AGENTS.md#board-rules) apply. Only what differs for this board is listed here.

