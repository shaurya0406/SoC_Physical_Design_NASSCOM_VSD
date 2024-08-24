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

### RISC-V GNU Toolchain
<details>
  <summary>
Expand or Collapse
  </summary>

The RISC-V GNU Toolchain is a collection of development tools for RISC-V architectures, including compilers, assemblers, and linkers. It is essential for developing software for RISC-V processors. Here’s a detailed overview of the RISC-V GNU Toolchain, including its installation and usage:

#### **RISC-V GNU Toolchain Overview**

The RISC-V GNU Toolchain provides a suite of tools necessary for building and debugging RISC-V software. The primary components of this toolchain include:

1. **Compiler (GCC - GNU Compiler Collection):**
   - Converts high-level source code (like C or C++) into assembly language or machine code specific to RISC-V architecture.

2. **Assembler (GNU Assembler - GAS):**
   - Translates assembly language code into machine code. 

3. **Linker (GNU Linker - LD):**
   - Combines object files into a single executable, resolving addresses and linking libraries as needed.

4. **Debugger (GDB - GNU Debugger):**
   - Allows for debugging of RISC-V programs, including setting breakpoints and inspecting variables.

5. **Libraries (Newlib or glibc):**
   - Provides standard library functions for C and C++ programs.

### **Installation of RISC-V GNU Toolchain**

#### **1. Prerequisites:**

- **Dependencies:** You need to have essential build tools and libraries. On a Linux system, you can typically install them using package managers like `apt` or `yum`.

```bash
# For Debian-based systems
sudo apt-get update
sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex
```

#### **2. Downloading the Toolchain:**

You can either build the toolchain from source or download pre-built binaries. For most users, downloading pre-built binaries is quicker.

- **Pre-Built Binaries:** You can find these on the [RISC-V GitHub releases page](https://github.com/riscv/riscv-gnu-toolchain/releases) or other trusted sources.

- **Building from Source:**

1. **Clone the Toolchain Repository:**

```bash
git clone https://github.com/riscv/riscv-gnu-toolchain.git
cd riscv-gnu-toolchain
```

2. **Build the Toolchain:**

```bash
# For a standard build
./configure --prefix=/path/to/installation
make
```

3. **Install the Toolchain:**

```bash
make install
```

   Replace `/path/to/installation` with the directory where you want to install the toolchain.

#### **3. Verifying Installation:**

After installation, ensure that the toolchain binaries are in your `PATH` and verify their versions:

```bash
riscv64-unknown-elf-gcc --version
riscv64-unknown-elf-gdb --version
```

### **Usage of RISC-V GNU Toolchain**

#### **1. Compiling a Program:**

To compile a C program for RISC-V, use the `riscv64-unknown-elf-gcc` command:

```bash
riscv64-unknown-elf-gcc -o my_program my_program.c
```

- `-o my_program`: Specifies the output file name.
- `my_program.c`: The source file to compile.

#### **2. Assembling and Linking:**

For assembly language files, use `riscv64-unknown-elf-as` and `riscv64-unknown-elf-ld`:

```bash
# Assemble
riscv64-unknown-elf-as -o my_program.o my_program.s

# Link
riscv64-unknown-elf-ld -o my_program my_program.o
```

#### **3. Debugging:**

Use `riscv64-unknown-elf-gdb` to debug your RISC-V program:

```bash
riscv64-unknown-elf-gdb my_program
```

Inside GDB, you can set breakpoints, run the program, and inspect variables.

##### Object Dump Command
The objdump command is used to display various types of information from object files and executables. Here’s how you can use it with the RISC-V GNU Toolchain:
```bash
riscv64-unknown-elf-objdump [options] file
```
`file`: The path to the object file or executable you want to examine.

`options`: `--disassemble-all` Disassemble all sections that contain executable code.

#### **4. Running the Program:**

To run your compiled RISC-V program, you'll need a RISC-V emulator or hardware. Common emulators include:

- **QEMU:** A versatile emulator that can emulate RISC-V architecture.

```bash
qemu-riscv64 my_program
```

- **Spike:** The RISC-V functional simulator.

```bash
spike pk my_program
```
</details>

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

# Day 1: SK1 | Lecture 3 - From Software Applications to Hardware

**1. Introduction**

- **Overview:** The lecture explores the transition from application software to hardware, focusing on how high-level applications are converted into machine language that can be executed by hardware.
- **Objective:** Understand the process that takes software applications and translates them into a format that hardware can execute, emphasizing the role of instruction set architecture (ISA).

**2. Software and Hardware Interaction**

- **Application Software:** Applications (e.g., stopwatch app) run on hardware inside devices like laptops.
- **System Software:** Converts application software into binary language understood by hardware. The system software stack includes:
  - **Operating System (OS):** Manages memory, I/O operations, and converts application code into assembly language.
  - **Compiler:** Translates high-level code (C/C++) into assembly language instructions specific to the hardware architecture (e.g., RISC-V).
  - **Assembler:** Converts assembly instructions into machine code (binary language).

**3. Compilation Process**

- **High-Level Code to Machine Code:**
  1. **Source Code:** Written in high-level languages (e.g., C, C++). For example, a stopwatch app function.
  2. **Compiler:** Converts the high-level source code into assembly language instructions for a specific architecture (e.g., RISC-V).
  3. **Assembler:** Converts assembly language into binary machine code (1s and 0s).
  4. **Execution:** The binary code is fed into hardware, which executes the instructions and performs the desired functions.

**4. Instruction Set Architecture (ISA)**

- **Definition:** ISA is the abstract interface between software and hardware, defining the set of instructions that a processor can execute.
- **RISC-V Example:** In a RISC-V architecture, the ISA includes instructions that the hardware understands and executes. The ISA acts as a language for communication between the software and the hardware.

**5. Hardware Description Language (HDL)**

- **Purpose:** Converts binary patterns into hardware logic. For example, if a binary pattern represents an addition operation, the hardware performs this operation on registers.
- **RTL (Register Transfer Level):** Describes the hardware implementation of the ISA in terms of registers and the operations between them.
- **Synthesis:** Translates the RTL description into a gate-level netlist (e.g., using logic gates, flip-flops).
- **Physical Design:** Converts the gate-level netlist into a physical layout (chip design) using standard design flows.

**6. Course Structure**

- **Part 1A: RISC-V Instructions and Architecture:** Focuses on understanding RISC-V ISA and its implications.
- **Part 1B:** Application of RISC-V in real-world scenarios and deeper dives into specific applications.
- **Future Parts:** Cover RTL design, synthesis, and physical design implementation.

**7. Summary**

- **Concepts Covered:**
  - Transition from application software to binary machine code.
  - Role of ISA in bridging software and hardware.
  - Process of designing hardware from ISA to physical chip layout.
- **Next Steps:** The course will delve deeper into RISC-V architecture and its practical applications.


# Day 1: SK2 | Lecture 1 - Open Source Digital ASIC Design using OpenLane

## Table of Contents
1. [Introduction](#introduction)
2. [Overview of OpenLane](#overview-of-openlane)
3. [Three Enablers of Open-Source ASIC Design](#three-enablers-of-open-source-asic-design)
   - [1. Open-Source RTL Designs](#1-open-source-rtl-designs)
   - [2. Open-Source EDA Tools](#2-open-source-eda-tools)
   - [3. Open-Source PDK](#3-open-source-pdk)
4. [Importance of the Process Design Kit (PDK)](#importance-of-the-process-design-kit-pdk)
5. [Relevance of 130nm Technology](#relevance-of-130nm-technology)
6. [ASIC Design Flow](#asic-design-flow)
7. [Getting Started with OpenLane](#getting-started-with-openlane)
8. [Resources](#resources)

---

## Introduction

Welcome to the Open Source Digital ASIC Design using OpenLane documentation. This guide is designed to walk you through the concepts and processes introduced in the workshop, providing a comprehensive understanding of how to design and implement digital ASICs using open-source tools.

## Overview of OpenLane

OpenLane is an open-source toolchain that facilitates digital ASIC design from RTL (Register Transfer Level) to GDSII (the final layout format used for fabrication). The workshop introduces OpenLane's features and use models, focusing on the implementation of Strive S, a RISC-V based CPU.

## Three Enablers of Open-Source ASIC Design

Designing a 100% open-source, fabrication-ready digital ASIC requires the integration of three critical components:

### 1. Open-Source RTL Designs
There are numerous open-source RTL (Register Transfer Level) designs available on platforms like [OpenCores.org](https://opencores.org/), [LibreCores.org](https://librecores.org/), and [GitHub](https://github.com/). These designs are essential building blocks for digital ASIC design.

### 2. Open-Source EDA Tools
Electronic Design Automation (EDA) tools are vital for automating the design process. Key open-source EDA tools include:
- **Spice Simulator**
- **Magic**: A VLSI layout tool.
- **OpenROAD**: A project providing tools for the entire RTL-to-GDS flow.
- **Qflow**: A digital synthesis toolchain.

### 3. Open-Source PDK
The Process Design Kit (PDK) is a set of files and documents essential for IC fabrication. The Skywater 130nm PDK, released in collaboration with Google, is the first open-source PDK available to the public, enabling fully open-source ASIC design.

## Importance of the Process Design Kit (PDK)

The PDK provides the necessary information for designing and fabricating ICs, including:
- **Device Models**
- **Technology Information**
- **Design Rules**
- **Standard Cell Libraries**
- **I/O Libraries**

Historically, PDKs were only available under non-disclosure agreements (NDAs), limiting their accessibility. The release of the Skywater 130nm PDK marks a significant milestone in democratizing IC fabrication.

## Relevance of 130nm Technology

Despite being an older process node, the 130nm technology is still widely used in various applications due to its:
- **Adequate Performance**: Suitable for many modern applications.
- **Lower Fabrication Costs**: More affordable compared to advanced nodes like 5nm or 7nm.

Examples of successful products using 130nm technology include the Intel Pentium 4 Extreme Edition, which ran at 3.5 GHz, and a RISC-V single-cycle CPU implemented in the Skywater 130nm process, capable of running at over 300 MHz.

## ASIC Design Flow

The ASIC design process is complex, involving multiple steps that need to be executed in a specific sequence. The flow integrates various tools to convert a design from RTL to GDSII. Here’s a high-level overview:

1. **RTL Design**: The functional description of the ASIC.
2. **Synthesis**: Converting the RTL to a gate-level netlist.
3. **Place and Route (PnR)**: Arranging the gates and connecting them.
4. **Verification**: Ensuring the design meets all specifications.
5. **GDSII Generation**: Final layout generation for fabrication.

OpenLane provides a cohesive environment to manage these steps, allowing designers to focus on optimizing their designs rather than managing tool interoperability.

## Getting Started with OpenLane

To begin working with OpenLane, follow these steps:

1. **Clone the OpenLane Repository**:
   ```bash
   git clone https://github.com/The-OpenROAD-Project/OpenLane.git
   cd OpenLane
   ```

2. **Set Up the Environment**:
   Follow the setup instructions in the [OpenLane README](https://github.com/The-OpenROAD-Project/OpenLane#readme) to install dependencies and prepare your environment.

3. **Run Your First Design**:
   Use the provided example designs to familiarize yourself with the OpenLane flow. Detailed instructions are available in the [documentation](https://github.com/The-OpenROAD-Project/OpenLane/blob/master/docs/README.md).

## Resources

- [OpenLane GitHub Repository](https://github.com/The-OpenROAD-Project/OpenLane)
- [Skywater 130nm PDK GitHub Repository](https://github.com/google/skywater-pdk)
- [OpenROAD Project](https://theopenroadproject.org/)
- [Qflow Documentation](http://opencircuitdesign.com/qflow/index.html)
- [Magic VLSI Layout Tool](http://opencircuitdesign.com/magic/)

# Day 1: SK2 | Lecture 2 - Simplified RTL to GDSII Flow for ASIC Design

## Table of Contents
1. [Introduction](#introduction)
2. [Overview of the RTL to GDSII Flow](#overview-of-the-rtl-to-gdsii-flow)
3. [Major Steps in the ASIC Design Flow](#major-steps-in-the-asic-design-flow)
   - [1. Synthesis](#1-synthesis)
   - [2. Floorplanning](#2-floorplanning)
   - [3. Placement](#3-placement)
   - [4. Clock Tree Synthesis (CTS)](#4-clock-tree-synthesis-cts)
   - [5. Routing](#5-routing)
   - [6. Sign-Off and Verification](#6-sign-off-and-verification)
4. [Additional Concepts](#additional-concepts)
   - [Standard Cell Libraries](#standard-cell-libraries)
   - [Process Design Kit (PDK)](#process-design-kit-pdk)
   - [Routing Layers in SKY130 PDK](#routing-layers-in-sky130-pdk)

---

## Introduction

This documentation provides a detailed overview of the RTL to GDSII flow for ASIC design, based on the SKY130 process technology. The RTL2GDS flow is a crucial part of digital integrated circuit (IC) design, transforming high-level design models into ready-to-fabricate layouts.

## Overview of the RTL to GDSII Flow

The RTL to GDSII flow represents the steps taken to transform a design from a high-level hardware description (RTL) to a physical layout (GDSII) that can be fabricated. This process involves several key stages: Synthesis, Floorplanning, Placement, Clock Tree Synthesis, Routing, and Sign-Off Verification.

## Major Steps in the ASIC Design Flow

### 1. Synthesis

**Objective**: Translate the RTL design into a gate-level netlist using standard cells from a library.

- **Input**: RTL (Register Transfer Level) description of the design.
- **Output**: Gate-level netlist.
- **Process**: The RTL is synthesized into a circuit composed of standard cells. These cells are pre-designed and characterized components available in the standard cell library.
- **Tools**: Yosys, Design Compiler.

### 2. Floorplanning

**Objective**: Define the physical layout of the design by partitioning the die and planning the power distribution network.

- **Chip Floorplanning**:
  - **Die Partitioning**: The chip area is divided among different components.
  - **Power Planning**: A robust power distribution network is created using VDD and ground pins connected through rings and metal straps to minimize IR drop and electromigration.
- **Macro Floorplanning**:
  - **Macro Dimensioning**: Define the dimensions and pin locations of macros.
  - **Routing Tracks Definition**: Determine the rows and routing tracks for later placement and routing steps.
- **Tools**: OpenROAD, Floorplan tools.

### 3. Placement

**Objective**: Place the synthesized standard cells onto the chip layout.

- **Global Placement**:
  - **Objective**: Find optimal positions for all cells, minimizing interconnect delays.
  - **Outcome**: Initial cell placement, potentially overlapping or illegal.
- **Detailed Placement**:
  - **Objective**: Adjust cell positions from global placement to ensure no overlaps and adherence to design rules.
  - **Outcome**: Legal cell placement ready for routing.
- **Tools**: OpenROAD, RePlace.

### 4. Clock Tree Synthesis (CTS)

**Objective**: Create a clock distribution network that delivers the clock signal to all clocked elements (e.g., flip-flops) with minimal skew and latency.

- **Clock Tree Structure**:
  - **Design**: The clock tree is constructed like a tree with the clock source as the root and the clocked elements as the leaves.
  - **Optimization**: Ensure that the clock signal reaches all elements at the same time (minimized skew).
- **Tools**: TritonCTS, Clockwise.

### 5. Routing

**Objective**: Connect the placed cells using metal layers while adhering to design rules.

- **Signal Routing**:
  - **Global Routing**: Coarse routing to create routing guides.
  - **Detailed Routing**: Fine-grained routing based on guides to implement actual connections.
- **Routing Constraints**: Utilize the available metal layers as defined by the PDK, respecting their thickness, pitch, and minimum width.
- **Tools**: FastRoute, OpenROAD Router.

### 6. Sign-Off and Verification

**Objective**: Ensure that the final layout meets all design and manufacturing requirements.

- **Design Rule Checking (DRC)**:
  - **Objective**: Verify that the layout adheres to manufacturing design rules.
- **Layout Versus Schematic (LVS)**:
  - **Objective**: Ensure that the layout matches the original gate-level netlist.
- **Static Timing Analysis (STA)**:
  - **Objective**: Confirm that all timing constraints are met to ensure proper operation at the target clock frequency.
- **Tools**: Magic, OpenSTA.

### 7. Export GDSII 
In this step, the final layout of the design is exported in the GDSII format, which is the industry-standard file format for IC layout data. This file contains all the necessary geometric shapes, layer information, and other essential data needed for fabricating the ASIC.

The command to export the GDSII file in OpenLANE typically involves finalizing the layout after routing and performing sign-off checks to ensure there are no violations. Once the checks pass, the GDSII file is generated and ready for tape-out.

## Additional Concepts

### Standard Cell Libraries

Standard cells are pre-designed logic gates with defined electrical characteristics. They are the building blocks of the synthesized netlist.

- **Cell Layout**: Regular, enclosed by a fixed-height rectangle, with a variable but discrete width.
- **Cell Views**:
  - **Timing (Liberty)**: Delay and power models.
  - **Layout (GDSII, LEF)**: Detailed and abstract physical layouts.
  - **Behavioral (HDL)**: Functional description.

### Process Design Kit (PDK)

The PDK provides the necessary technology files, design rules, and libraries required for IC design and fabrication.

- **Contents**:
  - **Device Models**: Electrical characteristics of the devices.
  - **Design Rules**: Guidelines for manufacturing.
  - **Standard Cell Libraries**: Pre-characterized logic gates.
- **SKY130 PDK**: An open-source PDK developed by SkyWater and Google for the 130nm process node.

### Routing Layers in SKY130 PDK

The SKY130 PDK defines six routing layers:

1. **Local Interconnect**: Titanium nitride layer.
2. **Metal1 to Metal5**: Aluminum layers for routing, each with specific characteristics.

- **Grid Routing**: Utilizes the defined metal layers and routing grids to create connections between cells.
- **Tools**: Detailed routers in the OpenROAD flow.

# Day 1: SK2 | Lecture 3 - Introduction to OpenLANE and Strive Chipsets

## Table of Contents
1. [Introduction](#introduction)
2. [OpenLANE ASIC Flow](#openlane-asic-flow)
   - [1. What is OpenLANE?](#1-what-is-openlane)
   - [2. Key Features of OpenLANE](#2-key-features-of-openlane)
   - [3. Supported Technologies](#3-supported-technologies)
   - [4. Modes of Operation](#4-modes-of-operation)
   - [5. Design Space Exploration](#5-design-space-exploration)
   - [6. Example Designs](#6-example-designs)
3. [Strive Chipsets](#strive-chipsets)
   - [1. Overview of the Strive Family](#1-overview-of-the-strive-family)
   - [2. Strive 1](#2-strive-1)
   - [3. Strive 2](#3-strive-2)
   - [4. Strive 2A](#4-strive-2a)
   - [5. Strive 3](#5-strive-3)
   - [6. Strive 5](#6-strive-5)
   - [7. Strive 6](#7-strive-6)
4. [Getting Started with OpenLANE](#getting-started-with-openlane)
   - [1. Installation and Setup](#1-installation-and-setup)
   - [2. Running Your First Design](#2-running-your-first-design)

---

## Introduction

This documentation provides an in-depth overview of OpenLANE, an open-source ASIC implementation flow, and the Strive family of chipsets. The OpenLANE flow is designed to simplify the process of creating digital ASICs, providing a streamlined, open-source alternative to commercial EDA tools.

## OpenLANE ASIC Flow

### 1. What is OpenLANE?

OpenLANE is an open-source ASIC implementation flow designed to provide a reference methodology for digital ASIC design using open-source EDA tools. It was developed as part of the open-source PDK initiative at Efabless and aims to produce clean GDSII layouts with minimal manual intervention.

- **License**: Apache 2.0
- **Public Repository**: [OpenLANE GitHub Repository](https://github.com/The-OpenROAD-Project/OpenLane)

### 2. Key Features of OpenLANE

- **Open Source**: Fully open-source and free to use with the Apache 2.0 license.
- **No Human in the Loop**: Aims to produce GDSII layouts with no LVS, DRC, or timing violations.
- **Autonomous and Interactive Modes**: Can be run in a push-button (autonomous) mode or step-by-step (interactive) mode.
- **Design Space Exploration**: Automatically finds the best set of flow configurations based on the design.

### 3. Supported Technologies

OpenLANE is tuned for the SkyWater 130nm PDK (SKY130), and it has been tested with the XFAB 180nm and GlobalFoundries 130nm PDKs.

- **Primary Target**: SKY130 PDK
- **Other Supported Technologies**: XFAB 180nm, GlobalFoundries 130nm

### 4. Modes of Operation

- **Autonomous Mode**: A push-button flow where the user configures the flow and waits for the final GDSII output.
- **Interactive Mode**: Allows users to run commands step-by-step, enabling experimentation and analysis of intermediate results.

### 5. Design Space Exploration

OpenLANE offers a feature called Design Space Exploration, which automatically sweeps through different configurations to find the optimal set of parameters for a given design.

- **Purpose**: To identify the best settings for flow configurations automatically.
- **Use Case**: Especially useful when working with new designs or for optimizing existing designs.

### 6. Example Designs

OpenLANE includes a large number of design examples to help users get started. As of now, there are 43 designs available, with more being added incrementally.

- **Design Examples**: 43 designs with known best configurations.
- **Public Repository**: All designs are available in the public GitHub repo.

## Strive Chipsets

### 1. Overview of the Strive Family

The Strive family of chipsets was developed as part of the open-source initiative at Efabless. These chipsets are designed to be fully open, including open PDKs, EDA tools, and RTL.

- **Objective**: To create fully open-source chipsets using open PDKs, EDA tools, and RTL.
- **Members**: The Strive family includes several variants, each with different features and memory configurations.

### 2. Strive 1

- **Description**: The first member of the Strive family.
- **Key Features**:
  - Implemented using the SKY130 high-density standard cell library.
  - Includes 1KB of SRAM and a few peripherals.

### 3. Strive 2

- **Description**: Similar to Strive 1 but uses 1KB SRAM generated by the OpenRAM compiler instead of the pre-designed SRAM.
- **Key Features**:
  - Uses OpenRAM-generated SRAM.
  - Same architecture as Strive 1.

### 4. Strive 2A

- **Description**: A variant of Strive 2 with a different hierarchical design.
- **Key Features**:
  - Modified hierarchy to achieve 100% automation from RTL to GDSII.
  - Aims for full automation in the design flow.

### 5. Strive 3

- **Description**: Similar to Strive 1 but uses the MSU C standard cell library.
- **Key Features**:
  - Uses MSU C standard cell library instead of SKY130.
  - Identical architecture to Strive 1.

### 6. Strive 5

- **Description**: A variant of Strive 2 but includes 8KB of memory by using eight 1KB SRAM blocks generated by OpenRAM.
- **Key Features**:
  - 8KB of total SRAM (8 x 1KB blocks).
  - Uses OpenRAM-generated SRAM.

### 7. Strive 6

- **Description**: Similar to Strive 2 but includes design for testing (DFT) structures.
- **Key Features**:
  - Incorporates DFT structures.
  - Same architecture as Strive 2.

## Getting Started with OpenLANE

### 1. Installation and Setup

**Requirements**:
- Docker (for containerized flow)
- Access to the SKY130 PDK

**Steps**:
1. Clone the OpenLANE repository from GitHub.
2. Pull the necessary Docker images.
3. Set up the environment variables for the PDK.

```bash
git clone https://github.com/The-OpenROAD-Project/OpenLane.git
cd OpenLane
make pull-openlane
```

### 2. Running Your First Design

After setting up OpenLANE, you can run your first design by following these steps:

1. **Prepare the design**:
   - Place your RTL files in the appropriate directory.
2. **Configure the flow**:
   - Set the required configuration parameters.
3. **Run the flow**:
   - Use the provided `flow.tcl` script to run the design in either autonomous or interactive mode.

```bash
# Step 1: Mount the OpenLANE Docker container.
# This command mounts the OpenLANE container to the local file system, making the tools and environment available for use.
make mount

# Step 2: Navigate to the directory containing your design.
# Replace <your_design> with the name of your design directory. This directory should contain the RTL files and other necessary inputs.
cd designs/<your_design>

# Step 3: Run the OpenLANE flow on your design.
# The flow.tcl script is used to start the OpenLANE ASIC flow for your specific design. 
# Replace <your_design> with the actual name of your design.
# This script will execute the flow steps (like synthesis, floorplanning, placement, routing) based on the configurations set for your design.
flow.tcl -design <your_design>
```

4. **Check the results**:
   - Review the generated GDSII and reports for DRC, LVS, and timing.