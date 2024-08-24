# Digital VLSI SoC Design and Planning
## Powered by NASSCOM & VSD
This course is designed to guide participants through the entire process of SoC design, from the RTL netlist to the final tape-out. Using the open-source `130nm Google-SkyWater PDK` and `Openlane` flow, one will gain hands-on experience with industry-standard tools like `Yosys`, `OpenLANE`, `NGSpice`, `Magic`, and `OpenSTA`. The course emphasizes practical, chip tapeout-oriented learning, providing participants with real-life design experience and a comprehensive understanding of the automated `RTL2GDSII` process. With a focus on `RISC-V` architecture, standard cell design, and timing analysis, this course equips you with the skills necessary to succeed in modern IC design and fabrication.

# Day 1
Welcome to the documentation for Day 1 of the "Digital VLSI SoC Design and Planning" course. This document provides a comprehensive overview of the foundational aspects of ASIC design, including the RTL to GDSII flow, OpenLANE, and Strive chipsets.

## Table of Contents
1. [Introduction to ASIC Design](#introduction-to-asic-design)
2. [Overview of the RTL to GDSII Flow](#overview-of-the-rtl-to-gdsii-flow)
   - [RTL Synthesis](#rtl-synthesis)
   - [Design Exploration](#design-exploration)
   - [Testing Structure Insertion](#testing-structure-insertion)
   - [Physical Implementation](#physical-implementation)
   - [Antenna Rule Violation Handling](#antenna-rule-violation-handling)
   - [Sign-Off](#sign-off)
   - [Export GDSII](#export-gdsii)
3. [Introduction to OpenLANE](#introduction-to-openlane)
   - [Key Features of OpenLANE](#key-features-of-openlane)
   - [Supported Technologies](#supported-technologies)
   - [Modes of Operation](#modes-of-operation)
   - [Design Space Exploration](#design-space-exploration)
   - [Example Designs](#example-designs)
4. [Introduction to Strive Chipsets](#introduction-to-strive-chipsets)

---

## Introduction to ASIC Design

ASIC (Application-Specific Integrated Circuit) design is a process that involves creating customized integrated circuits tailored for specific applications. This process transforms a high-level design specification into a physical layout that can be fabricated. The key stages of ASIC design include:

1. **RTL (Register Transfer Level) Design**: Writing code that describes the functionality of the circuit.
2. **Synthesis**: Converting RTL code into a gate-level netlist.
3. **Physical Design**: Translating the netlist into a physical layout.
4. **Sign-Off**: Ensuring that the design meets all requirements before fabrication.

---

## Overview of the RTL to GDSII Flow

The RTL to GDSII flow involves several stages:

### RTL Synthesis

**Objective**: Transform RTL code into a gate-level netlist using standard cells.

- **Tool**: Yosys
- **Commands**:
  ```bash
  cd designs/<your_design>
  flow.tcl -design <your_design> -run_synthesis
  ```
- **Concepts**:
  - **Standard Cells**: Pre-designed circuit components used in ASIC design.
  - **Synthesis Strategies**: Optimization techniques to improve area, timing, or power.

### Design Exploration

**Objective**: Evaluate various design configurations to find the optimal synthesis strategy.

- **Commands**:
  ```bash
  flow.tcl -design <your_design> -run_synth_explore
  ```
- **Report**: Provides insights on area, delay, and violations for different configurations.

### Testing Structure Insertion

**Objective**: Insert scan chains and test structures to facilitate post-fabrication testing.

- **Tool**: Fault (optional)

### Physical Implementation

**Objective**: Convert the gate-level netlist into a physical layout.

- **Tools**: OpenROAD, TritonRoute
- **Sub-Steps**:
  - **Floor and Power Planning**: Define the chip layout and power distribution.
  - **Placement**: Arrange cells within the layout.
  - **Clock Tree Synthesis (CTS)**: Design a balanced clock distribution network.
  - **Routing**: Connect cells using metal layers.
- **Commands**:
  ```bash
  flow.tcl -design <your_design> -run_floorplan
  flow.tcl -design <your_design> -run_place
  flow.tcl -design <your_design> -run_cts
  flow.tcl -design <your_design> -run_route
  ```

### Antenna Rule Violation Handling

**Objective**: Manage long wire segments that can act as antennas and damage transistor gates.

- **Solutions**:
  - **Bridging**: Elevate wires to higher metal layers.
  - **Inserting Antenna Diodes**: Add diodes to dissipate charges.
- **Commands**:
  ```bash
  flow.tcl -design <your_design> -run_antennacheck
  ```

### Sign-Off

**Objective**: Verify that the design meets all manufacturing and timing requirements.

- **Tools**: Magic, OpenSTA, netgen
- **Sub-Steps**:
  - **DRC (Design Rule Checking)**: Check layout against manufacturing rules.
  - **LVS (Layout vs. Schematic)**: Verify layout matches the schematic.
  - **Timing Analysis**: Ensure timing constraints are met.
- **Commands**:
  ```bash
  flow.tcl -design <your_design> -run_drc
  flow.tcl -design <your_design> -run_lvs
  flow.tcl -design <your_design> -run_timing
  ```

### Export GDSII

**Objective**: Generate the GDSII file for fabrication.

- **Commands**:
  ```bash
  flow.tcl -design <your_design> -run_export_gdsii
  ```

---

## Introduction to OpenLANE

OpenLANE is an open-source ASIC implementation flow that automates the process of converting RTL designs into GDSII layouts. It integrates various open-source tools and aims to streamline ASIC design.

### Key Features of OpenLANE

- **Open Source**: Fully open-source and free to use with Apache 2.0 license.
- **No Human in the Loop**: Produces GDSII layouts with minimal manual intervention.
- **Autonomous and Interactive Modes**: Offers both push-button and step-by-step modes.
- **Design Space Exploration**: Automatically finds the best flow configurations.

### Supported Technologies

- **Primary Target**: SkyWater 130nm PDK (SKY130)
- **Other Supported Technologies**: XFAB 180nm, GlobalFoundries 130nm

### Modes of Operation

- **Autonomous Mode**: Push-button operation to generate GDSII files.
- **Interactive Mode**: Step-by-step commands for detailed experimentation.

### Design Space Exploration

OpenLANE’s Design Space Exploration feature helps in optimizing design configurations by automatically evaluating different settings.

### Example Designs

OpenLANE provides numerous design examples to help users get started, with 43 designs available.

---

## Introduction to Strive Chipsets

The Strive family of chipsets is part of an open-source initiative, providing examples of different aspects of ASIC design. Each variant demonstrates unique features and design techniques.

### Strive 1

- **Description**: Initial member of the Strive family.
- **Features**: 1KB of SRAM and peripherals, using the SKY130 high-density standard cell library.

### Strive 2

- **Description**: Similar to Strive 1, but with SRAM generated by OpenRAM.
- **Features**: Uses OpenRAM-generated SRAM with the same architecture as Strive 1.

### Strive 2A

- **Description**: Variant of Strive 2 with a modified hierarchical design for full automation.
- **Features**: Achieves 100% automation from RTL to GDSII.

### Strive 3

- **Description**: Similar to Strive 1, but uses the MSU C standard cell library.
- **Features**: Identical architecture to Strive 1 with a different standard cell library.

### Strive 5

- **Description**: Enhanced version of Strive 2 with 8KB of memory.
- **Features**: Includes eight 1KB SRAM blocks generated by OpenRAM.

### Strive 6

- **Description**: Similar to Strive 2 but includes Design for Test (DFT) structures.
- **Features**: Same architecture as Strive 2 with additional test structures.

---
