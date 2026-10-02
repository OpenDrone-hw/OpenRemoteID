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
`research/` is sourced reference material: a competitor claim or a component
datasheet does not establish product behaviour.

## Repo

| | |
|---|---|
| Status | See the `status-*` topic on the repo. Never written here. |
| Designed in | KiCad 10 |
| KiCad project | `hardware/OpenRemoteID.kicad_pro` |
| Root schematic | `hardware/OpenRemoteID.kicad_sch` |
| Board | `hardware/OpenRemoteID.kicad_pcb`, 2 copper layers, 1.6 mm |
| Local library | `hardware/lib.kicad_sym`, `hardware/lib.pretty/`, `hardware/lib.3dshapes/`, nickname `lib` |
| Shared library | `hardware/KiCad-Library/`, submodule of [OpenDrone-hw/KiCad-Library](https://github.com/OpenDrone-hw/KiCad-Library), nickname `OpenDrone`; exact component datasheets resolve through the project text variable `OPENDRONE_LIB` |
| Local datasheets | Linked from `hardware/DESIGN.md` "Datasheets"; no PDFs are vendored |
| Design boundary | `hardware/DESIGN.md` |
| License | CERN-OHL-S-2.0 |

## Environment

```sh
# schematic and board checks
kicad-cli sch erc hardware/OpenRemoteID.kicad_sch
kicad-cli pcb drc --schematic-parity --refill-zones hardware/OpenRemoteID.kicad_pcb
git diff --check

# netlist, for scripted analysis
kicad-cli sch export netlist --format kicadsexpr -o /tmp/OpenRemoteID.net hardware/OpenRemoteID.kicad_sch
```

Report exact ERC and DRC results. Findings only become release-approved
through the reviewed limits in the OpenDrone
[release standard](https://github.com/OpenDrone-hw/.github/blob/main/RELEASES.md);
new types and increased counts block release preparation. On macOS
`kicad-cli` is at `/Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli`;
`KPY` is KiCad's bundled Python,
`/Applications/KiCad/KiCad.app/Contents/Frameworks/Python.framework/Versions/Current/bin/python3`.

## Rules

Identical in every OpenDrone board repo. Do not edit here; edit the template.

- **Never text-edit** `.kicad_sch`, `.kicad_pcb` or `.kicad_dru`. Use KiCad, or
  kicad-skip / the pcbnew API for scripted changes. `.kicad_pro` is JSON and may
  be edited directly for metadata.
- **Metadata yes, connections no.** An agent may write BOM and documentation
  fields (MPN, Manufacturer, LCSC, Cost, Datasheet, text variables). An agent
  may not change nets, wiring, routing, placement, footprint assignment, or any
  value that changes the circuit.
- **Close KiCad before any write to a KiCad file.** KiCad caches library tables
  at process start and overwrites files on save.
- **Reuse before you draw.** Check the `OpenDrone` library and its
  `PARTS-USED.md` first. If the part is there we have already sourced,
  footprinted and shipped it, and its symbol links to the exact committed
  datasheet: place it from `OpenDrone`. Draw a new part into `lib` only when
  the catalogue has nothing that fits, imported with
  `easyeda2kicad` from its LCSC number. Pulling a newer catalogue is a
  deliberate, reviewed commit: `git submodule update --remote
  hardware/KiCad-Library`, then DRC.
- **One person holds a board layout at a time.** KiCad files do not merge. Say
  on Discord that you are taking it. See [CONTRIBUTING.md](CONTRIBUTING.md).
- **Run ERC and DRC before every pull request.** Existing approved findings
  may remain; a new type or increased count must be reviewed before merge.
  Commands are in Environment above.

## By task

Board-specific paths are in Environment above. `KPY` is KiCad's bundled
Python named there.

- Check the design: run the ERC and DRC commands in Environment before every pull request.
- Add a part: place it from the `OpenDrone` library if `hardware/KiCad-Library/PARTS-USED.md` lists it; otherwise import it into `lib` with `$KPY <hardware-tooling>/hardware/kicad/import_part.py` (read `--help` first), KiCad closed.
- Render the board for the README: `$KPY <hardware-tooling>/hardware/kicad/render_board.py hardware/OpenRemoteID.kicad_pcb --outdir images`, KiCad closed.
- Analyse the netlist: export it with the netlist command in Environment, then read it with a script; never hand-write a second BOM.
- Update the shared library: `git submodule update --remote hardware/KiCad-Library`, run DRC, commit as its own reviewed change.
