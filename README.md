# Digital VLSI SoC Design and Planning
## Powered by NASSCOM & VSD
This course is designed to guide participants through the entire process of SoC design, from the RTL netlist to the final tape-out. Using the open-source `130nm Google-SkyWater PDK` and `Openlane` flow, one will gain hands-on experience with industry-standard tools like `Yosys`, `OpenLANE`, `NGSpice`, `Magic`, and `OpenSTA`. The course emphasizes practical, chip tapeout-oriented learning, providing participants with real-life design experience and a comprehensive understanding of the automated `RTL2GDSII` process. With a focus on `RISC-V` architecture, standard cell design, and timing analysis, this course equips you with the skills necessary to succeed in modern IC design and fabrication.

# SKY130 - Day 1: Lecture 1 - Introduction to QFN 48 Package, Chip, Pads, Core, Die, and IPs

## Overview

This lecture introduces the basic concepts of chip design using the example of an Arduino board. The focus is on understanding the transition from board-level design to chip-level design, with an emphasis on the QFN48 package.

## Key Concepts and Technical Terms

### 1. **QFN48 Package**
   - **Quad Flat No-Lead (QFN) Package**: A type of IC package with no leads, often used in surface-mount technology.
   - **Wire Bonds**: Connections between the chip and the package using fine wires.

### 2. **Chip Components**
   - **Pads**: Interfaces on the chip for signals to enter and exit.
   - **Core**: The central area where digital logic (gates, muxes, etc.) resides.
   - **Die**: The physical silicon piece on which the chip components are fabricated.

### 3. **Foundry IPs**
   - **Foundry**: A manufacturing facility where chips are produced.
   - **Intellectual Property (IP)**: Pre-designed functional blocks (e.g., PLL, ADC, SRAM) provided by the foundry for integration into the chip.
   - **Macros**: Pre-designed digital blocks used in chip design.

### 4. **Communication with Foundry**
   - **Interface Files**: Files provided by the foundry to help communicate design specifications and requirements for chip fabrication.

## Additional Notes

- **Foundry vs. Macros**: While both are pre-designed blocks, IPs require more specialized knowledge to create, hence the term "Intellectual Property."
- The lecture emphasizes the importance of understanding and correctly implementing these foundational concepts in chip design.