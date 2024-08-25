# Digital VLSI SoC Design and Planning
## Powered by NASSCOM & VSD
This course is designed to guide participants through the entire process of SoC design, from the RTL netlist to the final tape-out. Using the open-source `130nm Google-SkyWater PDK` and `Openlane` flow, one will gain hands-on experience with industry-standard tools like `Yosys`, `OpenLANE`, `NGSpice`, `Magic`, and `OpenSTA`. The course emphasizes practical, chip tapeout-oriented learning, providing participants with real-life design experience and a comprehensive understanding of the automated `RTL2GDSII` process. With a focus on `RISC-V` architecture, standard cell design, and timing analysis, this course equips you with the skills necessary to succeed in modern IC design and fabrication.

# Day 1
Welcome to the documentation for Day 1 of the "Digital VLSI SoC Design and Planning" course. This document provides a comprehensive overview of the foundational aspects of ASIC design, including the RTL to GDSII flow, OpenLANE, and Strive chipsets.

## Theoretical Concepts
For Detailed analysis of each lecture of Day 1, refer to [Day1.md](Day1.md)
### Day1 Overview
<details>
  <summary> 
Expand or Collapse
  </summary>

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

</details>

## Lab Details

### Part 1: Introduction to OpenLANE and the Flow.tcl Script

This section introduces you to the OpenLANE flow, its purpose, and how it automates the RTL-to-GDSII flow. We will also dive into the `flow.tcl` script, which is a key component in running the OpenLANE flow, and discuss the differences between interactive and non-interactive sessions, as well as the initial steps required to set up the environment.

---

#### **1. Overview of OpenLANE**

**OpenLANE** is an open-source flow designed to facilitate the process of converting a Register Transfer Level (RTL) design into a final GDSII layout, which is ready for tape-out. The flow is designed to be automated, modular, and reusable, making it easier for designers to work through the complex stages of physical design.

- **Purpose**: The primary goal of OpenLANE is to provide a completely open-source, end-to-end ASIC design flow that integrates multiple open-source tools. This includes tools for synthesis, placement, routing, and other necessary stages in the RTL-to-GDSII process.

- **Key Tools Used**:
  - **Yosys**: For logic synthesis.
  - **ABC**: For technology mapping.
  - **OpenSTA**: For Static Timing Analysis (STA).
  - **Magic**: For layout generation and DRC.
  - **Klayout**: For layout viewing and further checks.
  - **Netgen**: For LVS (Layout vs. Schematic) checking.
  - **OpenROAD**: For place and route.
  - **OpenPhySyn**: For physical synthesis optimizations.

- **Flow Steps**: OpenLANE breaks down the design process into several stages:
  1. **Preparation**: Setting up the environment and merging libraries.
  2. **Synthesis**: Converting the RTL code into a gate-level netlist.
  3. **Floorplanning**: Defining the chip's size, shape, and placement of I/O pins.
  4. **Placement**: Placing the standard cells in the defined floorplan.
  5. **Clock Tree Synthesis (CTS)**: Creating a clock distribution network.
  6. **Routing**: Connecting all the placed cells with wires.
  7. **Signoff**: Performing final checks, including DRC, LVS, and timing analysis.

---

#### **2. Flow.tcl Script**

The `flow.tcl` script is the backbone of the OpenLANE flow. It is used to run the entire flow in a sequential manner or interactively, depending on the user's requirements.

- **Script Location**: The `flow.tcl` script is located in the root directory of the OpenLANE flow. It is the primary script that orchestrates the entire design flow by calling various tools and scripts in a defined order.

- **Modes of Operation**:
  - **Interactive Mode**: The user can execute each step of the flow manually, providing more control and the ability to analyze results after each step.
  - **Non-Interactive Mode**: The entire flow runs automatically from start to finish with minimal user intervention. This mode is useful for running the entire design flow in a batch process.

- **Command Structure**:
  - In **interactive mode**, the user runs the `flow.tcl` script with the `-interactive` flag:
    ```bash
    ./flow.tcl -interactive
    ```
  - Once in interactive mode, commands can be issued step by step, such as:
    ```bash
    prep design <design_name>
    run_synthesis
    ```
  - In **non-interactive mode**, the flow runs from start to finish using a single command:
    ```bash
    ./flow.tcl -design <design_name>
    ```

- **Key Steps in the Script**:
  1. **Preparation (`prep`)**: The script sets up the environment and merges the required technology libraries, such as LEF (Library Exchange Format) files.
  2. **Synthesis (`run_synthesis`)**: Executes the Yosys synthesis tool to generate a gate-level netlist.
  3. **Floorplanning (`run_floorplan`)**: Runs the floorplanning step, defining the physical dimensions and layout of the chip.
  4. **Placement (`run_placement`)**: Places the synthesized cells onto the defined floorplan.
  5. **CTS (`run_cts`)**: Synthesizes the clock tree, ensuring proper clock distribution across the design.
  6. **Routing (`run_routing`)**: Connects the cells using metal layers to form the complete design.
  7. **Signoff (`run_signoff`)**: Runs final checks like DRC and LVS before the design is taped out.

- **Flexibility and Customization**:
  - The `flow.tcl` script allows for significant flexibility, as users can modify and add new commands depending on the design requirements. 
  - Configuration files can be edited to change the flow's behavior, such as adjusting utilization rates or modifying clock constraints.
  
- **Command Logging**:
  - All commands executed during the flow are logged in a `commands.log` file within the `runs` directory, providing a complete record of the flow for debugging and review.

---

### Part 2: Setting Up the OpenLANE Environment and Running the Initial Steps

In this part, we'll dive into the process of setting up the OpenLANE environment and the initial steps required to begin working with a specific design. This includes cloning the necessary repositories, setting up the Process Design Kit (PDK), and understanding the significance of different design configuration files. We will also walk through the process of running the `flow.tcl` script in interactive mode, and discuss the importance of each step in the early stages of the design flow.

---

#### **1. Setting Up the Environment**

Before you can start working with OpenLANE, you need to set up your environment properly. This involves installing the necessary tools, cloning the required repositories, and configuring the Process Design Kit (PDK).

- **Cloning the Repositories**:
  - The first step is to clone the OpenLANE repository from GitHub, which contains all the scripts and tools needed for the flow.
    ```bash
    git clone https://github.com/The-OpenROAD-Project/OpenLane.git
    ```
  - After cloning the repository, you must also clone the PDK repository, typically the SkyWater 130nm PDK, which includes all the design rules and libraries needed for the specific process technology.
    ```bash
    git clone https://github.com/google/skywater-pdk.git
    ```
  - These repositories provide all the necessary components to start the design process.

- **Setting Up the PDK**:
  - The Process Design Kit (PDK) is crucial as it contains the physical design rules and standard cell libraries for the process node you’re targeting (e.g., SkyWater 130nm).
  - In the OpenLANE environment, the PDK setup involves integrating these libraries with the design tools in a manner that allows the tools to use them during synthesis, placement, routing, and other steps.
  - To set up the PDK within OpenLANE, navigate to the `OpenLane` directory and run the following command:
    ```bash
    make mount
    ```
  - This command mounts the PDK and tools into a Docker container, ensuring that the environment is isolated and properly configured.

- **Checking the Environment**:
  - Once the PDK is set up, it’s important to ensure that the environment is correctly configured. This can be done by running:
    ```bash
    ./flow.tcl -interactive
    ```
  - If the environment is correctly set up, the interactive session will start without any errors, and you’ll be ready to run the design flow.

---

#### **2. Understanding the Configuration Files**

The OpenLANE flow relies heavily on various configuration files that define how the flow should behave for a specific design. Understanding these files is critical for controlling the design process.

- **Configuring `config.tcl`**:
  - The `config.tcl` file is the main configuration file that controls the behavior of the flow for a specific design.
  - It includes parameters such as the target frequency, synthesis strategy, placement density, and routing strategies.
  - Users can edit this file to fine-tune the flow according to the needs of their design. For example, you might want to change the target clock period to meet specific timing requirements:
    ```tcl
    set ::env(CLOCK_PERIOD) "10"
    ```
  - Other important parameters include utilization factors, which control the density of the cells in the design, and various tool-specific options that can affect the synthesis, placement, and routing outcomes.

- **Merging LEF Files**:
  - LEF (Library Exchange Format) files describe the physical dimensions and pin placements of standard cells and macros.
  - During the setup process, these LEF files are merged to create a complete view of all the cells and blocks that will be used in the design. This merging process is critical to ensure that the placement and routing tools have the necessary information to work with the standard cells.
  - The LEF files are typically merged in the preparation step using:
    ```bash
    prep -design <design_name>
    ```
  - This command prepares the design by merging the required LEF files and setting up the design environment.

- **Design-Specific Settings**:
  - The `config.tcl` file is not the only place where configurations are stored. Each design might have specific settings files that further control how the flow behaves.
  - For example, `sky130A_sram_1kbyte_1rw1r_32x256_8.v` might define the specific SRAM configuration used in a design, ensuring that the correct memory models are used during simulation and synthesis.

---

#### **3. Running the Initial Steps in Interactive Mode**

After setting up the environment and configuring the design, the next step is to run the initial stages of the flow. These stages include design preparation, synthesis, and floorplanning.

- **Starting the Interactive Session**:
  - Begin by launching the interactive session:
    ```bash
    ./flow.tcl -interactive
    ```
  - This opens a prompt where you can enter commands to run each step of the flow manually.

- **Preparation (`prep`)**:
  - The first command to run is the preparation step:
    ```bash
    prep -design <design_name>
    ```
  - This command prepares the design environment by merging the LEF files, setting up the necessary directories, and preparing the configuration files.
  - The preparation step also involves setting up the `runs` directory, where all the output files will be stored. Each run generates a timestamped folder under `runs`, which contains subdirectories for temporary files, results, reports, and logs.

- **Synthesis (`run_synthesis`)**:
  - After preparation, the next step is to run synthesis:
    ```bash
    run_synthesis
    ```
  - This command invokes Yosys and ABC to convert the RTL code into a gate-level netlist.
  - The synthesis step is critical as it determines the quality of the netlist, which directly impacts the subsequent steps like placement and routing.
  - The output of the synthesis step includes a synthesized netlist and reports on timing, area, and other critical metrics.

- **Floorplanning (`run_floorplan`)**:
  - The next command is to run floorplanning:
    ```bash
    run_floorplan
    ```
  - Floorplanning defines the chip’s size, shape, and placement of key components such as macros and I/O pins.
  - The outcome of the floorplanning step is a layout with defined regions for standard cells and macros, which serves as the foundation for the placement and routing stages.

- **Importance of Order**:
  - It is crucial to run these steps in the correct order because each step depends on the output of the previous one. For instance, if you skip the synthesis step and try to run floorplanning, the command will fail because the required netlist is missing.

---
