# Low-Voltage DC Motor Driver Board

Dual H-bridge carrier for 6–10.8 V brushed DC motors with current sense, protection and instrumentation.

This repository contains a KiCad-editable reference design intended for a junior PCB designer portfolio. It is a preliminary engineering design, not a certified or production-released product.

## Design brief

- **Difficulty:** Advanced
- **Revision:** A
- **Target board:** 2-layer FR-4, 1 oz copper, 50 x 40 mm target outline
- **Design status:** schematic and PCB source included; fabrication outputs are preliminary and require a final KiCad review.

## Main specifications

- DRV8833RTY dual H-bridge in WQFN-16
- 6–10.8 V recommended motor supply; 11.8 V absolute maximum
- Two motor outputs or one bipolar stepper interface
- Per-bridge current-sense resistors and test points
- Reverse-polarity protection MOSFET and TVS at VM input
- 2-layer FR-4, 1 oz copper, 50 x 40 mm target outline

## Repository layout

- `drv8833-low-voltage-motor-driver.sch` — editable KiCad legacy schematic source.
- `drv8833-low-voltage-motor-driver.kicad_pcb` — editable KiCad PCB source.
- `drv8833-low-voltage-motor-driver.kicad_pro` — KiCad project metadata.
- `BOM.csv` — component list with manufacturer part numbers.
- `images/` — readable schematic and placement renders.
- `manufacturing/` — preliminary Gerber and drill set.
- `docs/` — design notes and bring-up checklist.

## Key design decisions

The datasheet specifies 1.5 A RMS/DC per bridge under stated conditions, but this design does not claim a safe continuous current. Final current must be derated from package, copper area, ambient temperature, motor duty cycle and measured thermal rise.

The layout target is two layers with a continuous ground plane on the bottom layer. Use 0.20 mm signal traces, 0.50 mm low-voltage power traces where practical, and at least 0.20 mm clearance for a standard low-cost fabrication process. Increase copper width for high-current paths after calculating temperature rise. Place connectors on board edges, keep polarity and signal names on silkscreen, and provide labeled test points.

## Verification status

KiCad was not available in the execution environment, so **ERC and DRC were not run**. No claim of ERC/DRC pass is made. Before ordering, open the project in KiCad, update symbols and footprints from the installed libraries, run ERC and DRC, resolve every warning, verify the netlist and inspect the antenna/thermal areas.

## Post-fabrication test checklist

1. Inspect solder joints, connector orientation, polarity markings and antenna keepout.
2. With no power applied, measure resistance between every supply rail and GND; investigate any low resistance before powering.
3. Power through a current-limited bench supply. Confirm input current is within the expected no-load range.
4. Measure the regulated rail before attaching the functional load.
5. Verify test points and interface signals with a DMM or oscilloscope.
6. For motor hardware, start with a current-limited supply and no mechanical load; measure bridge temperature and current during the actual duty cycle.

**Executed tests:** file generation and structural checks only. **Not executed:** KiCad ERC/DRC, electrical bring-up, RF performance, thermal validation, USB compliance, and motor-load testing.

## BOM

| Ref | Description | Value | Package | Manufacturer / MPN |
|---|---|---|---|---|
| J1 | VM/GND motor supply | 2-pin 5.08mm | TerminalBlock_1x02 | Phoenix Contact 1729018 |
| U1 | Dual H-bridge motor driver | WQFN-16 | DRV8833RTY | Texas Instruments DRV8833RTY |
| Q1 | Reverse polarity protection | PowerPAK SO-8 | P-MOSFET | AO4407A |
| D1 | Motor rail transient clamp | SMBJ | SMBJ12A | Littelfuse SMBJ12A |
| R1 | Bridge A current sense | 0.1 Ohm | R_2512 | Vishay WSL2512R1000FEA |
| R2 | Bridge B current sense | 0.1 Ohm | R_2512 | Vishay WSL2512R1000FEA |
| C1 | VM bulk decoupling | 47uF 25V | C_1206 | Panasonic EEU-FR1E470 |
| C2 | VM ceramic bypass | 100nF | C_0805 | Murata GRM21BR71E104KA01 |
| C3 | VCP charge pump | 10nF | C_0805 | Murata GRM21BR71H103KA01 |
| C4 | VINT bypass | 2.2uF | C_0805 | Murata GRM21BR60J225ME39 |
| J2 | Motor A/B outputs | 4-pin 5.08mm | TerminalBlock_1x04 | Phoenix Contact 1729028 |
| J3 | Logic: AIN1/AIN2/BIN1/BIN2/SLEEP/FAULT | 1x06 2.54mm | PinHeader_1x06 | Samtec TSW-106-07-G-S |
| TP1 | VM current sense test point | TH | TestPoint | Keystone 5011 |
| TP2 | AISEN test point | TH | TestPoint | Keystone 5011 |
| TP3 | BISEN test point | TH | TestPoint | Keystone 5011 |

## Primary sources

- [Texas Instruments DRV8833 datasheet](https://www.ti.com/lit/ds/symlink/drv8833.pdf)
- [Texas Instruments DRV8833 product page](https://www.ti.com/product/DRV8833)
- [Vishay WSL power metal strip resistors](https://www.vishay.com/docs/30108/wsl.pdf)

## Manufacturing notes

Use the supplied Gerbers only as a review artifact. The current PCB source contains a placement/routing skeleton and must be opened in KiCad for final footprint assignment, net connectivity, filled zones, design-rule setup, and verified fabrication export.
