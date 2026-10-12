# OpenRemoteID

Remote ID hardware concept: ESP32-C3-MINI-1 radio module and ATGM336H GNSS receiver.

Validate: `kicad-cli sch erc hardware/OpenRemoteID.kicad_sch && kicad-cli pcb drc --schematic-parity --refill-zones hardware/OpenRemoteID.kicad_pcb`

## Boundaries

- Sourcing (suppliers, prices, quotes, RFQs, contacts) never lives in OpenDrone repositories.
- Never text-edit `.kicad_sch`, `.kicad_pcb` or `.kicad_dru`: use KiCad, or kicad-skip / the pcbnew API with KiCad closed. `.kicad_pro` is JSON and may be edited for metadata.
- Agents write metadata fields only (MPN, Manufacturer, LCSC, Datasheet, text variables), never nets, wiring, routing, placement, footprint assignment or circuit values.
- KiCad libraries stay project-local; import parts with `easyeda2kicad` only.
- KiCad files do not merge: one person holds a board layout at a time.

## Board boundaries

- Claim no certification, compliance, approval, current draw, RF range, board size or BOM cost without evidence in this repository; `hardware/DESIGN.md` states what is implemented versus intent.

## Pointers

- Shared parts catalogue: `hardware/KiCad-Library/PARTS-USED.md`
- Release standard: https://github.com/OpenDrone-hw/.github/blob/main/RELEASES.md
