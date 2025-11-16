# YoRadio – PCB (v0.4) for SSD1322 display

![PCB – view 1](img/PCB1.jpg)
![PCB – view 2](img/PCB2.jpg)

Hardware project of a printed circuit board (PCB) for YoRadio. The repository contains the complete KiCad project and ready-to-fabricate files (Gerbers + drill), as well as screenshots and board photos.

Status: stable v0.4 (fabrication files in the YR_v0.4 directory and the YR_v0.4.zip archive)

Note: Polish version available in README.pl.md

## Table of Contents
- Overview
- Repository contents
- Requirements and tools
- Quick start (KiCad)
- Fabrication files (Gerber/Drill)
- Assembly (BOM, stencil)
- Generating fabrication outputs
- Previews
- Versioning and backups
- License and disclaimers
- Contributing and issue reporting

## Overview

- Two-layer printed circuit board project for YoRadio.
- KiCad files allow editing the schematic and PCB and generating new fabrication outputs.
- The repository includes photos and screenshots of the project, as well as a Bill of Materials (BOM).

Note: The `myoptions_0.4.h` file is a firmware/software configuration header, included for convenience. It is not required to fabricate the PCB itself.

## Repository contents

Key files and directories:
- KiCad project:
  - `YR.kicad_pro` — KiCad project
  - `YR.kicad_sch` — schematic
  - `YR.kicad_pcb` — PCB layout
  - `schematic.pdf` — schematic in PDF format (view without KiCad)
- Fabrication (Gerber/Drill) — ready to send to the PCB manufacturer:
  - Directory: `YR_v0.4/`
  - Archive: `YR_v0.4.zip`
- Bill of Materials (BOM):
  - `YR.csv`
- Models/3D and graphics:
  - `YR.wrl` — 3D model (KiCad 3D Viewer)
  - `img/` — photos and screenshots (e.g., `PCB1.jpg`, `PCB2.jpg`)
- Project backups:
  - `YR-backups/` — automatic zip snapshots of the project

Other:
- `fp-info-cache` — footprint cache
- `YR.kicad_prl` — session/project settings
- `myoptions_0.4.h` — firmware configuration file (auxiliary)

## Requirements and tools

- KiCad 7/8 (latest stable release from series 7 or 8 recommended).
- To generate Gerber/Drill files: KiCad’s built-in tools (Plot/Generate Drill Files).
- Gerber viewer (e.g., KiCad’s built-in Gerber Viewer) — optional for verification.

## Quick start (KiCad)

1. Open the project: `YR.kicad_pro`.
2. Review the schematic: `YR.kicad_sch` (or `schematic.pdf` if you don’t have KiCad).
3. Open the PCB: `YR.kicad_pcb` (check layers and DRC rules).
4. 3D preview (optional): View → 3D Viewer (model `YR.wrl`).

## Fabrication files (Gerber/Drill)

Ready to send to the PCB manufacturer (version v0.4):
- Directory: `YR_v0.4/`
- Archive: `YR_v0.4.zip` (contains the same files, convenient to upload to the manufacturer)

Typical contents:
- Copper layers: `YR-F_Cu.gbr`, `YR-B_Cu.gbr`
- Solder masks: `YR-F_Mask.gbr`, `YR-B_Mask.gbr`
- Solder paste (stencil): `YR-F_Paste.gbr`, `YR-B_Paste.gbr` (if assembled on both sides)
- Silkscreen: `YR-F_Silkscreen.gbr`, `YR-B_Silkscreen.gbr`
- Board outline: `YR-Edge_Cuts.gbr`
- Drill files: `YR-PTH.drl`, `YR-NPTH.drl` (+ maps `*_drl_map.gbr`)
- Job file: `YR-job.gbrjob` (fabrication metadata from KiCad)

Recommended order parameters (typical, confirm with your manufacturer):
- Layer count: 2
- Material: FR4, 1.6 mm thickness (standard)
- Copper: 1 oz (35 µm)
- Solder mask: green (or other) + white silkscreen
- Finish: HAL Sn/Pb or lead-free HAL/ENIG per preference
- Minimum tracks/clearances/hole sizes: as per project DRC settings (check in KiCad)

## Assembly (BOM, stencil)

- BOM: `YR.csv` — parts list for procurement.
- Stencil: for SMD assembly, use the `*_Paste.gbr` files to manufacture a solder paste stencil.
- Note: ensure component orientations (diodes, electrolytics, ICs) match the polarity/orientation markers on the silkscreen.

## Programming the ESP32 Module

The ESP32 module is programmed using a USB–UART interface with a 3.3V logic level.
After connecting the interface and powering the board, press two buttons: RST and BOOT, then release them in the following order: first RST, then BOOT.
This will start the bootloader, which allows the module to be programmed directly from the Arduino IDE

## Generating fabrication outputs (from KiCad)

If you make changes and want to refresh the outputs:
1. PCB Editor → File → Plot…
   - Format: Gerber
   - Select layers: F_Cu, B_Cu, F_Mask, B_Mask, F_Paste, B_Paste, F_Silkscreen, B_Silkscreen, Edge.Cuts
   - Ensure the Plot format options meet your fab’s requirements (e.g., use vector font).
2. PCB Editor → File → Fabrication Outputs → Drill Files…
   - Generate `PTH.drl` and `NPTH.drl`.
3. Verify completeness and correctness in the Gerber Viewer (KiCad).
4. Zip the files and send them to your manufacturer.

## Previews

Sample photos and screenshots:
- `img/PCB1.jpg`
- `img/PCB2.jpg`
- `img/Screenshot_2025-11-09_18-42-12.png`
- `img/Screenshot_2025-11-09_18-42-12_mod.png`
- Real board photos: `img/20251109_183416.jpg`, `img/20251109_183430.jpg`, `img/20251109_183437.jpg`, `img/20251109_183449.jpg`

Example embeds:
![PCB – view 1](img/PCB1.jpg)
![PCB – view 2](img/PCB2.jpg)

## Versioning and backups

- Current version: v0.4 (directory `YR_v0.4/`, archive `YR_v0.4.zip`).
- Automatic backups: `YR-backups/` (with date and time).
- Recommendation: after significant changes, regenerate Gerber/Drill files and tag as a new version (e.g., v0.5).

## License and disclaimers

- License: there is no explicit license file in the repository — if you intend to share/use the project, choose and add a `LICENSE` (e.g., CERN-OHL, MIT, other).
- Disclaimer: the project is provided in good faith, without warranty. Use at your own risk; verify the design against your requirements and standards.

## Contributing and issue reporting

- Want to improve the project or add a feature? Open a Pull Request.
- Bugs/notes: create an Issue in the repository and include:
  - problem description,
  - project version (e.g., v0.4),
  - screenshots/photos or log files (if applicable).

Enjoy using the YoRadio PCB project!
