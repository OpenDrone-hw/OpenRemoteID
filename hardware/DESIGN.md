# OpenRemoteID design boundary

This document separates the checked-in design from intended behaviour. The
KiCad files are authoritative for implemented hardware.

## Checked-in hardware

`OpenRemoteID.kicad_sch` and `OpenRemoteID.kicad_pcb` contain these placed
devices:

| Reference | Value | Intended role |
| --- | --- | --- |
| `U2` | ESP32-C3-MINI-1-N4 | processor and 2.4 GHz radio |
| `U3` | ATGM336H-5NR-32 | GNSS receiver |
| `LDO2` | ME6211C33M5G-N | 5 V to 3.3 V regulation |
| `RF2` | CONUFL001-SMD-T | GNSS antenna connector |
| `SW2` | B3U-1000P | user input |
| `LED2` | 16-213/GHC-YR1S1/3T | status indication |

The PCB is 1.6 mm, two copper layers, with six footprints and no tracks, vias or
copper zones. The schematic is not electrically complete: KiCad 10 reports 85
errors and one warning. Values, pin assignments, board dimensions, current
draw, BOM price and RF performance are therefore not treated as verified
product specifications.

## Design intent

The concept is a standalone module that derives 3.3 V from a 5 V input, obtains
position and time from the GNSS receiver, and broadcasts Remote ID messages from
the ESP32-C3. Intended external interfaces are 5 V, ground, UART RX/TX and a
passive GNSS antenna on U.FL. Firmware and its protocol behaviour are not
implemented in this repository.

## Validation baseline

Run checks with KiCad 10:

```sh
kicad-cli sch erc --exit-code-violations hardware/OpenRemoteID.kicad_sch
kicad-cli pcb drc --schematic-parity --exit-code-violations hardware/OpenRemoteID.kicad_pcb
```

The current ERC baseline is 85 errors and one warning. There is no passing DRC,
manufacturing package, prototype measurement, firmware test or regulatory test
evidence in the repository.

## Regulatory boundary

ASTM F3411 and EN 4709-002 are design targets. Do not describe the module as
compliant, certified, approved or legal for sale until product-level evidence
and the required declarations exist. Component approvals are input evidence,
not a finished-product conclusion.
