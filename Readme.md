# 10 GHz LNA — KiCad 8 Project

This project contains the schematic and layout for a low-noise amplifier designed for 10 GHz amateur radio applications. It uses a packaged pHEMT MMIC, SMA connectors, and Rogers 4003C substrate.

## Features
- MMIC-based gain stage
- Biasing network with gate protection
- RF input/output with SMA pads
- Designed for low noise figure and stable gain

## Files
- `10GHz_LNA.sch`: KiCad schematic
- `10GHz_LNA.kicad_pro`: Project file
- `BOM.txt`: Parts list
- `Footprints/`: Custom pads
- `Notes/`: Layout and impedance guidance


# Power Supply
(VIN_5V) ──┐
           ├─► MCP1700-3302E (U2)
           │     ├─ IN → VIN_5V
           │     ├─ OUT → LDO_OUT
           │     └─ GND → GND
           │
           └─► LDO_OUT ──┬────┐
                         │    │
                      ┌──┴┐  ┌▼──┐
                      │C5 │  │C6 │
                      └───┘  └───┘
                      22nF   0.1µF
                         │     │
                         └─────┴─► GND

# Power Switch
LDO_OUT ──► P-MOSFET (Q1)
             ├─ Source → LDO_OUT
             ├─ Drain → MMIC_VCC
             └─ Gate ─┐
                     ├─► 10kΩ pull-up to LDO_OUT
                     └─► Drain of N-MOSFET (Q2)

SEQUENCER_CTRL ─► Gate of N-MOSFET (Q2)
                    ├─ Source → GND
                    └─ 330Ω series resistor

# MMIC Block
MMIC_VCC ──► Pin 1 (BGA2800)
           ├─► Decoupling Caps: C1 (22nF), C2 (0.1µF), C3 (10µF) → GND

RF_IN ──► 100pF cap (C4) ──► Pin 6 (Input)
RF_OUT ◄── 100pF cap (C7) ◄── Pin 3 (Output)

Pin 2, 4, 5 → GND

# Net Labels
- VIN_5V: 5V Input
- LDO_OUT: Regulated 3.3V
- MMIC_VCC: Switched 3.3V to MMIC
- SEQUENCER_CTRL: Arduino digital output
- RF_IN: Input signal net
- RF_OUT: Output signal net
