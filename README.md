# Digital VLSI SoC Design and Planning
## Powered by NASSCOM & VSD
This course is designed to guide participants through the entire process of SoC design, from the RTL netlist to the final tape-out. Using the open-source `130nm Google-SkyWater PDK` and `Openlane` flow, one will gain hands-on experience with industry-standard tools like `Yosys`, `OpenLANE`, `NGSpice`, `Magic`, and `OpenSTA`. The course emphasizes practical, chip tapeout-oriented learning, providing participants with real-life design experience and a comprehensive understanding of the automated `RTL2GDSII` process. With a focus on `RISC-V` architecture, standard cell design, and timing analysis, this course equips you with the skills necessary to succeed in modern IC design and fabrication.

# SKY130 - Day 1: SK1 | Lecture 1 - Introduction to QFN 48 Package, Chip, Pads, Core, Die, and IPs

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

# SKY130 - Day 1: SK1 | Lecture 2 - Introduction to RISC-V

## Overview
This lecture introduces the RISC-V Instruction Set Architecture (ISA) and outlines the flow from high-level programming to hardware execution. The key concepts covered include the role of ISA, the process of compiling code, and the translation from software to hardware.

## **Key Points Covered:**

### 1. **Introduction to ISA:**
   - **Definition:** An ISA is a language through which software communicates with hardware. It defines the set of instructions that the hardware can execute.
   - **Role:** It acts as the interface between high-level programming languages and the underlying hardware.

### 2. **From C Program to Hardware:**
   - **High-Level Program:** A C program is written at the software level.
   - **Compilation Process:**
     - **Assembly Language:** The C program is first compiled into an assembly language specific to the RISC-V ISA.
     - **Machine Language:** The assembly code is then translated into machine language, which consists of binary code (0s and 1s) that the hardware can understand.
     - **Execution:** The binary code is executed by the hardware, producing the desired output.

### 3. **Hardware Description Language (HDL):**
   - **Role of HDL:** To implement the RISC-V ISA specifications in hardware, a hardware description language (HDL) is used. This is crucial for designing and simulating the hardware.
   - **Example:** The lecture uses a Pwith 32 CPU core as an example of implementing RISC-V specifications in HDL.

### 4. **RTL to Layout Flow:**
   - **RTL (Register Transfer Level):** Represents the design at a level where the flow of data between registers is described.
   - **Layout:** The RTL design is eventually translated into a physical layout that can be manufactured on silicon.

### 5. **End-to-End Flow:**
   - **Starting Point:** The process begins with the RISC-V architecture specification.
   - **Implementation:** The architecture is implemented using RTL.
   - **Final Product:** The RTL design is converted into a physical layout, which is used to manufacture the hardware that will execute the compiled binary code.

### 6. **Next Steps:**
   - **Future Lectures:** The course will delve deeper into the application of these concepts, transitioning from software applications to hardware design and execution.
   - **Focus:** Future videos will explore the journey from high-level applications to the chip level in more detail.
