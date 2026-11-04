# LORA_MOD_V1.0
This board has been made to run on 24V 5A DC supply. Main triggering pulse provided by MCU to trigger the N Channel MOSFET, that controls pneumatic at output side.
2 pin white connector is used for MCUs GPIO connection and 2 pin Green-screw connector used for INPUT and OUTPUT connection

# Features
Holtek HT66F0185 MCU (24-SSOP) as the main controller
Leirda WB28 LoRa module for long-range wireless communication
U.FL / IPEX antenna connector (J4) (CONUFL001-SMD)
UART0 header (J3) – 4-pin JST-XH, for external communication
Programming header (J2) – 5-pin JST-XH, for flashing the MCU
On-board 3.3 V regulation (LM1117-3.3)
Reverse-polarity protection diode on the supply input (D1, M7)
Diode-isolated TXD/RXD lines between the header and the MCU (D7, D8 with 2.7 kΩ resistors)
2-layer PCB with ground pour, two mounting holes

# Block Diagram
 5V (J3 / J2) ──► D1 (M7) ──► LM1117-3.3 ──► +3V3 ──┬──► HT66F0185 (U2)
                                                    └──► Leirda WB28 (U1) ──► J4 (antenna)

 J3 (UART0) ◄──► D7/D8 + R2/R3 ◄──► HT66F0185 ◄── UART ──► WB28 (COMMU_RXD / COMMU_TXD)
 J2 (Prog.) ───► SWDIO / SWCLK / NRESET ───────► HT66F0185


 # Connectors
 J3 – UART0 (4-pin JST-XH, B4B-XH-A)
Pin	Signal	Notes
1	GND	Ground
2	TXD	Serial line (via D8 / R3 to MCU)
3	RXD	Serial line (via D7 / R2 to MCU)
4	+5V	Supply input (through D1)

J2 – Programming (5-pin JST-XH, B5B-XH-A)
Pin	Signal	Notes
1	+5V	
2	SWDIO	Debug/programming data
3	SWCLK	Debug/programming clock
4	NRESET	Reset (10 kΩ pull-up to 3V3)
5	GND	Ground

J4 – Antenna
U.FL (IPEX) connector for the LoRa antenna. Never power or transmit without an antenna attached.

# Bill of Materials
Ref	Value	Description / Package
U1	Leirda WB28	LoRa module
U2	HT66F0185-24SSOP	Holtek MCU
U3	LM1117-3.3	3.3 V LDO regulator (SOT-223)
D1	M7	Rectifier diode, reverse-polarity protection
D7, D8	1N4148W	Signal diodes (SOD-123)
R1, R4	10 kΩ	Reset pull-ups (SMD)
R2, R3	2.7 kΩ	UART line resistors (SMD)
C1	2.2 µF	MCU VDD decoupling
C2	0.1 µF	LoRa module decoupling
C3	0.22 µF	LoRa module decoupling
C4	100 nF	3V3 decoupling
C6, C7	47 µF	Bulk capacitors (regulator input/output, electrolytic)
C11	1 µF	3V3 decoupling (electrolytic)
J2	B5B-XH-A	5-pin programming header
J3	B4B-XH-A(LF)(SN)	4-pin UART header
J4	CONUFL001-SMD	U.FL antenna connector

# Specifications
Parameter	Value
Input voltage	5 V DC
Logic / module voltage	3.3 V
Regulator	LM1117-3.3 (800 mA max)
MCU	Holtek HT66F0185, 24-SSOP
Wireless	LoRa (Leirda WB28)
Board size	approx. 55 × 35 mm (update with actual size)
Layers	2
Design tool	Altium Designer

# Repository Structure
.
├── README.md
├── LICENSE
├── hardware/
│   ├── schematic/        # .SchDoc and PDF export
│   ├── pcb/              # .PcbDoc
│   ├── gerber/           # Gerber + drill files (ready for fabrication)
│   ├── bom/              # BOM (.xlsx / .csv)
│   └── pick_and_place/   # Centroid / XY file for assembly
├── firmware/             # HT66F0185 source code (Holtek HT-IDE3000)
├── datasheets/           # HT66F0185, LM1117, Leirda WB28 datasheets
└── images/
    ├── schematic.png
    ├── pcb_top.png
    ├── pcb_bottom.png
    ├── 3d_top.png
    └── 3d_bottom.png

# Getting Started
Fabricate the PCB using the files in hardware/gerber/.
Assemble using the BOM and pick-and-place files.
Attach the LoRa antenna to J4.
Program the MCU through J2 using the Holtek e-Link / e-WriterPro programmer (SWDIO/SWCLK/NRESET).
Power the board with a regulated 5 V supply (via J3 pin 4 or J2 pin 1).
Connect your host/device to the UART header J3 for external communication.

# Notes and Known Issues (V1.0)
Input must be a regulated 5 V DC. This board does not include a mains (AC) stage; use a certified isolated AC-DC adapter or module if running from mains.
Keep the antenna area of U1/J4 free of copper where possible, and check the LoRa module datasheet for the keep-out recommendation.
Some silkscreen labels overlap pads (C11, J2, D8). Clean up for the next revision.
Check peak LoRa TX current against the LM1117 capability and thermal limits (dropout from 5 V to 3.3 V is dissipated as heat).

# License
This project is licensed under the MIT License (hardware: consider CERN-OHL). See the LICENSE file.

# Author
Your Name GitHub: @your-username Email: your.email@example.com

# Acknowledgements
Holtek Semiconductor – HT66F0185 documentation
Leirda – WB28 LoRa module documentation
Texas Instruments / ST – LM1117 datasheet
