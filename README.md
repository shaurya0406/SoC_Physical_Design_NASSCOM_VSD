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
<details>
  <summary> 
Expand or Collapse
  </summary>
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

### Part 3: The `runs` Directory and Folder Structures

The `runs` directory and its associated folder structures play a crucial role in the OpenLANE flow. This part will provide a detailed explanation of the `runs` directory, the purpose of its subdirectories, and the contents generated during the design process. We'll cover the significance of each folder and how they contribute to managing and organizing the results of the design flow.

---

#### **1. Overview of the `runs` Directory**

When you start the OpenLANE flow, one of the first things the toolchain does is create a `runs` directory. This directory serves as a central repository for all the outputs generated during the design process. Each time you execute a flow, a new timestamped folder is created within the `runs` directory. This allows you to easily manage and reference the results of different design runs.

- **Timestamped Folder Creation**:
  - Each run creates a unique folder within the `runs` directory, named with the date and time of the run. This timestamped folder helps in distinguishing between multiple runs, making it easier to track the evolution of your design.
  - For example, a typical folder name might be something like `2024-08-25_14-30-00`, indicating the run started on August 25, 2024, at 2:30 PM.
  - This naming convention ensures that you can easily identify and access the results of specific runs without confusion.

---

#### **2. Subdirectories within the Timestamped Folder**

Each timestamped folder within the `runs` directory contains several important subdirectories. These subdirectories are organized to store different types of files generated at various stages of the design flow. Understanding the purpose of each subdirectory is essential for navigating the results of your design process.

- **1. `tmp` Directory**:
  - **Purpose**: The `tmp` directory is used to store temporary files generated during the design flow. These files are typically intermediate files that are necessary for the flow but may not be needed after the flow is complete.
  - **Contents**: This directory might include files such as intermediate netlists, temporary timing analysis reports, or logs from individual steps.
  - **Usage**: While these files are usually not critical for final analysis, they can be useful for debugging purposes or understanding the flow's behavior at a granular level.

- **2. `results` Directory**:
  - **Purpose**: The `results` directory is where the final output files from each step of the design flow are stored. These files represent the culmination of each stage, such as synthesized netlists, floorplans, and final GDSII files.
  - **Contents**: This directory is further divided into subfolders corresponding to each stage of the design flow, such as `synthesis`, `floorplan`, `placement`, `routing`, etc.
    - For example, after the synthesis step, the `results/synthesis` folder will contain the synthesized netlist and associated reports.
    - After the final step in the flow, the `results/routing` folder might contain the GDSII file, which is the final layout that can be sent for fabrication.
  - **Usage**: This directory is critical for reviewing the final outcomes of the flow. It allows you to examine the key deliverables of each stage, such as checking the quality of the netlist, the efficiency of the floorplan, or the correctness of the final layout.

- **3. `reports` Directory**:
  - **Purpose**: The `reports` directory stores all the reports generated during the flow, including timing analysis, area reports, power estimates, and more.
  - **Contents**: Similar to the `results` directory, this directory is divided into subfolders for each stage of the design flow. Each subfolder contains reports relevant to that particular stage.
    - For example, the `reports/synthesis` folder might include reports on the number of cells, the area utilization, and the critical path timing after synthesis.
    - The `reports/routing` folder might include detailed routing congestion reports or post-route timing analysis.
  - **Usage**: Reports are essential for evaluating the performance and quality of your design at each stage. They provide insights into how well the design meets its objectives, such as timing closure, area constraints, and power consumption.

- **4. `logs` Directory**:
  - **Purpose**: The `logs` directory contains log files for each step of the design flow. These logs record the commands executed, tool outputs, and any warnings or errors encountered during the run.
  - **Contents**: Like the other directories, `logs` is divided into subfolders for each stage of the design flow. Each subfolder contains log files that document the actions taken during that stage.
    - For instance, the `logs/synthesis` folder might contain a detailed log of the synthesis process, including the commands executed by Yosys and ABC, as well as any messages generated during the process.
    - The `logs/routing` folder might include logs from the detailed routing step, capturing the actions of the OpenROAD tools.
  - **Usage**: The logs are invaluable for debugging and understanding the behavior of the flow. If a step fails or produces unexpected results, the log files are the first place to look for clues about what went wrong.

---

#### **3. Key Files within the `runs` Directory**

Aside from the main subdirectories, the `runs` directory also contains several key files that provide additional information about the flow and its configuration.

- **1. `config.optical` File**:
  - **Purpose**: This file contains a snapshot of the configuration options used during the run. It records the parameters set in the `config.tcl` file and any modifications made during the interactive session.
  - **Contents**: The file lists all the environment variables and settings that were active during the run, including clock constraints, synthesis options, and placement density targets.
  - **Usage**: The `config.optical` file is useful for reviewing the exact configuration used in a particular run. If you need to replicate a successful run or understand the differences between runs, this file provides the necessary details.

- **2. `commands` File**:
  - **Purpose**: This file logs all the commands executed during the interactive session or automated flow. It provides a sequential record of the steps taken during the run.
  - **Contents**: The file includes every command executed, from design preparation to the final routing step. It captures the order of operations and any arguments passed to the commands.
  - **Usage**: The `commands` file is essential for tracing the flow of the design process. If you need to audit the steps taken during a run or replicate the flow, this file provides a detailed roadmap of the process.

---

### Part 4: Running Synthesis

#### **Overview of the Synthesis Step**

Synthesis is a crucial step in the RTL-to-GDSII flow where the high-level RTL (Register Transfer Level) description of the design is converted into a gate-level netlist. This process involves transforming the RTL code, written in hardware description languages like Verilog or VHDL, into a netlist consisting of logic gates and flip-flops that can be used for physical design. The synthesis process ensures that the design meets the specified functional and timing requirements.

#### **Understanding the Synthesis Command**

In OpenLANE, synthesis is initiated through the interactive mode or through specific commands in a non-interactive mode. Here's a breakdown of the synthesis process:

1. **Initiating Synthesis:**
   - In an interactive session, after preparing the design, you run the synthesis step using the command:
     ```tcl
     run_synthesis
     ```
   - This command triggers the synthesis process, which includes various tools and scripts to convert RTL code into a gate-level netlist.

2. **Synthesis Tools Involved:**
   - **Yosys:** An open-source synthesis tool that performs RTL synthesis. It processes the RTL code and generates an intermediate representation.
   - **ABC:** A tool used for technology mapping and logic optimization. It optimizes the netlist generated by Yosys to meet timing and area constraints.

3. **Files Generated During Synthesis:**
   - **Netlist Files:** The primary output is the gate-level netlist, which is used in subsequent steps. This file is usually stored in the `results` directory under a folder named `synthesis`.
   - **Synthesis Reports:** Reports detailing the synthesis results, including area, timing, and resource utilization, are generated and stored in the `reports` directory.

#### **Detailed Steps in the Synthesis Process**

1. **Preparation:**
   - Before running synthesis, ensure that the design environment is properly set up. This includes verifying that all necessary files and configurations are in place. The `design` folder should contain the RTL source files, configuration files, and any other required inputs.

2. **Running Synthesis:**
   - In an interactive OpenLANE session, you might run the following commands:
     ```tcl
     source flow.tcl
     run_synthesis
     ```
   - This command will start the synthesis process. During this step, the toolchain will perform the following tasks:
     - **RTL Parsing:** Yosys parses the RTL code to create an internal representation.
     - **Optimization:** Yosys performs initial optimizations on the RTL code.
     - **Mapping:** ABC maps the optimized RTL representation to technology-specific cells.
     - **Optimization and Mapping:** ABC further optimizes the design and maps it to the target technology's standard cell library.

3. **Monitoring the Synthesis Process:**
   - As synthesis progresses, monitor the OpenLANE logs for any errors or warnings. The logs can be found in the `logs` directory within the timestamped folder. Check these logs to ensure that the synthesis is proceeding as expected and to troubleshoot any issues that arise.

4. **Reviewing Synthesis Output:**
   - Once synthesis is complete, review the following files and reports:
     - **Netlist Files:** Located in the `results/synthesis` folder. These files represent the gate-level netlist.
     - **Synthesis Reports:** Found in the `reports/synthesis` folder. These reports include details such as the total area of the synthesized design, the number of cells used, and timing information.

#### **Post-Synthesis Analysis**

1. **Analyzing Synthesis Reports:**
   - Examine the synthesis report to understand the quality of the synthesis. Key metrics include:
     - **Area:** The total area occupied by the synthesized design.
     - **Cell Count:** The number of cells used in the design.
     - **Timing:** The critical path delay and other timing constraints.
   - Compare these metrics against the design specifications to ensure that the design meets the requirements.

2. **Flop Ratio Calculation:**
   - One of the first tasks after synthesis is to calculate the Flop Ratio. 
   - The Flop Ratio is a metric used to evaluate the utilization of flip-flops in your design.
   - It is calculated as the ratio of the number of D flip-flops to the total number of cells in the design.

    **Formula for Flop Ratio**

    To calculate the Flop Ratio, use the following formula:

    $$ \text{Flop Ratio} = \frac{\text{Number of D Flip-Flops}}{\text{Total Number of Cells}} $$

    **Example Calculation**

    Here’s a step-by-step guide to calculating the Flop Ratio using an example:

    1. **Obtain the Number of D Flip-Flops:**
    - This information is typically found in the synthesis report under the section detailing flip-flop counts.
    - **Example:** Number of D flip-flops = 1634

    2. **Obtain the Total Number of Cells:**
    - This can be found in the same synthesis report, under cell counts.
    - **Example:** Total number of cells = 17323

    3. **Perform the Calculation:**
    - Substitute the values into the formula:
        
    $$ \text{Flop Ratio} = \frac{1634}{17323} \approx 0.094 $$

    - Convert to percentage:

    $$ \text{Flop Ratio (Percentage)} = 0.094 \times 100 \approx 9.4\% $$

    4. **Interpreting the Result:**
    - A Flop Ratio of 9.4% indicates that 9.4% of the total cell count is comprised of D flip-flops.
    - **Importance:** A higher Flop Ratio can suggest more complex state management in the design, which might impact timing and area.

    5. **Importance of Flop Ratio**

    - **Design Efficiency:** Helps in evaluating how efficiently flip-flops are used in the design.
    - **Performance:** Affects the timing and performance of the design, as flip-flops are critical for synchronous operation.
    - **Optimization:** Provides insights into potential areas for optimization to reduce the number of flip-flops if necessary.


3. **Reviewing the Synthesized Netlist:**
   - Open the netlist files generated in the `results/synthesis` folder. Verify that the netlist accurately represents the RTL design and that all components are correctly mapped.

4. **Troubleshooting:**
   - If there are issues or discrepancies in the synthesized netlist or reports, revisit the RTL code and configuration files. Ensure that the design constraints and parameters are correctly specified.

</details>

## My Setup on Mac M2 Pro
- I have installed a `Ubuntu 22.04.02` Virtual Machine using [Parallels Desktop](https://www.parallels.com) (Will try to setup OpenLane directly on Mac later)
- Cloned OpenLane Github Repo and installed necessary requirements.

### Installation of required packages
Update packages database and upgrade the packages to avoid version mismatches then install required packages.
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv make git
```
### Docker Installation
Docker is required to run OpenLane because it ensures a consistent, isolated, and reproducible environment, simplifies the setup process, provides portability across different operating systems, allows easy version control, enhances security, and facilitates collaboration. By using Docker, developers can focus on the design process without worrying about the complexities of setting up and managing the underlying toolchain and dependencies
```bash
# Remove old installations
sudo apt-get remove docker docker-engine docker.io containerd runc

# Create the directory /etc/apt/keyrings with specific permissions (755: owner can read/write/execute; group/others can read/execute)
sudo install -m 0755 -d /etc/apt/keyrings

# Download the Docker GPG key and save it to /etc/apt/keyrings/docker.asc. This key is used to verify the integrity of Docker packages.
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

# Ensure the Docker GPG key file has read permissions for all users
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the Docker repository to the system's APT sources list, specifying the architecture and signing key
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Update the package list to include the Docker packages from the newly added repository
sudo apt-get update

# Install Docker Engine, CLI, container runtime, and necessary plugins (Buildx and Compose)
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Run a test Docker container to verify that Docker is installed and functioning correctly
sudo docker run hello-world

# Create the 'docker' group, which allows users in this group to run Docker commands without sudo
sudo groupadd docker

# Add the current user to the 'docker' group to enable running Docker commands without sudo
sudo usermod -aG docker $USER

# Reboot the system to apply group changes
sudo reboot

# After reboot, run the test Docker container again to verify that the current user can run Docker commands without sudo
docker run hello-world
```
A successful installation of Docker would have this output:
```plaintext
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

<img src="images/Day1/Docker_Hello_World.png" alt="Docker_Hello_World" width="100%"/>

### Checking Installation Requirements
In order to check the installation, you can use the following commands:
```bash
git --version
docker --version
python3 --version
python3 -m pip --version
make --version
python3 -m venv -h
```
Successful output will look like this:

```plaintext
git version 2.34.1
Docker version 27.1.2, build d01f264
Python 3.10.12
pip 22.0.2 from /usr/lib/python3/dist-packages/pip (python 3.10)
GNU Make 4.3
Built for aarch64-unknown-linux-gnu
Copyright (C) 1988-2020 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
usage: venv [-h] [--system-site-packages] [--symlinks | --copies] [--clear] [--upgrade] [--without-pip] [--prompt PROMPT] [--upgrade-deps] ENV_DIR [ENV_DIR ...]

Creates virtual Python environments in one or more target directories.

positional arguments:
  ENV_DIR               A directory to create the environment in.

options:
  -h, --help            show this help message and exit
  --system-site-packages
                        Give the virtual environment access to the system site-packages dir.
  --symlinks            Try to use symlinks rather than copies, when symlinks are not the default for the platform.
  --copies              Try to use copies rather than symlinks, even when symlinks are the default for the platform.
  --clear               Delete the contents of the environment directory if it already exists, before environment creation.
  --upgrade             Upgrade the environment directory to use this version of Python, assuming Python has been upgraded in-place.
  --without-pip         Skips installing or upgrading pip in the virtual environment (pip is bootstrapped by default)
  --prompt PROMPT       Provides an alternative prompt prefix for this environment.
  --upgrade-deps        Upgrade core dependencies: pip setuptools to the latest version in PyPI

Once an environment has been created, you may wish to activate it, e.g. by sourcing an activate script in its bin directory.
```
<img src="images/Day1/Check_Requirements.png" alt="Check_Requirements" width="100%"/>

## Download and Install OpenLane
Download OpenLane from GitHub:

These steps will download and build OpenLane and sky130 PDK. Finally, it will run a ~5 minute test of `spm` design that verifies that the flow and the PDK were properly installed. If you are planning to use another PDK, then you need to follow the PDK installation guide for that specific PDK.
```bash
git clone --depth 1 https://github.com/The-OpenROAD-Project/OpenLane.git
cd OpenLane/
make
make test
```
Successful test will output the following line:
```
Basic test passed
```
<img src="images/Day1/Make_Test.png" alt="Make_Test" width="100%"/>

## Viewing Test Design Outputs
Open the final layout using KLayout. This will open the window of KLayout in editing mode -e with sky130 technology.
```bash
# Enter a Docker session:
make mount

# Open the spm.gds using KLayout with sky130 PDK
klayout -e -nn $PDK_ROOT/sky130A/libs.tech/klayout/tech/sky130A.lyt \
   -l $PDK_ROOT/sky130A/libs.tech/klayout/tech/sky130A.lyp \
   ./designs/spm/runs/openlane_test/results/final/gds/spm.gds
```
<img src="images/Day1/Test_GDS.png" alt="Test_GDS" width="100%"/>

## Leave the Docker
```bash
exit
```

## Step 1. Starting the OpenLane Environment
OpenLane uses Docker to create a reproducible environment for your projects. You don’t need any extra steps to run the Docker image, as the Makefile already takes care of it. Just run the following commands to enter the OpenLane environment:
```bash
cd ~/OpenLane/
make mount
```
Your terminal environment should now switch to the OpenLane Container:

<img src="images/Day1/OpenLane_Container.png" alt="OpenLane_Container" width="100%"/>

## Step 2. Running the flow
The entry point for OpenLane is the `./flow.tcl` script.

For various arguments to this script, checkout the [Docs](https://openlane.readthedocs.io/en/latest/reference/openlane_commands.html#general-commands)
```bash
# Run in Interactive mode
./flow.tcl -interactive
```
The terminal prompt should now change to Tcl Console represeted by `%` symbol:

<img src="images/Day1/Flow_Tcl_Console.png" alt="Flow_Tcl_Console" width="100%"/>

## Step 3. Setup Target Package
```bash
# Specify OpenLane Package Version
package require openlane 0.9
```
## Step 4. Specify the Target Design
Specify the design folder. A design folder should contain a `config.tcl` or `config.json` file defining the design parameters. If the folder is not found, the `./designs` directory is searched for said file.

In our case, we will be working on `picorv32a` already present in the `~/Openlane/designs` directory.
```bash
prep -design picorv32a
```
Output:

<img src="images/Day1/Prep_Design_Tcl.png" alt="Prep_Design_Tcl" width="100%"/>

## Prep Design Output Explanation

The output of the `prep -design picorv32a` command in OpenLane is providing detailed information about the preparation of the design environment for the physical design flow of the `picorv32a` design. 

Note: this output may vary according to the Github commit version of OpenLane you are using.

### 1. `[INFO]: Using configuration in 'designs/picorv32a/config.tcl'...`
- **Explanation**: This message indicates that OpenLane is using the configuration file located at `designs/picorv32a/config.tcl`. This file contains specific settings and parameters that guide the design flow for the `picorv32a` design.

### 2. `[INFO]: Process Design Kit: sky130A`
- **Explanation**: The Process Design Kit (PDK) being used is `sky130A`. A PDK includes technology-specific information like design rules, process parameters, and standard cell libraries. `sky130A` refers to the SkyWater 130nm process technology.

### 3. `[INFO]: PDK Root: /home/parallels/.volare`
- **Explanation**: The root directory for the PDK is located at `/home/parallels/.volare`. This is where the PDK files and related data are stored. OpenLane accesses these files for process-specific information during the flow.

### 4. `[INFO]: Standard Cell Library: sky130_fd_sc_hd`
- **Explanation**: The standard cell library being used is `sky130_fd_sc_hd`. This library contains the logic cells (like gates, flip-flops) that are used to build the design. `hd` typically stands for high-density, indicating a library optimized for area.

### 5. `[INFO]: Optimization Standard Cell Library: sky130_fd_sc_hd`
- **Explanation**: The same `sky130_fd_sc_hd` library is also being used for optimization purposes. Optimization in physical design often involves choosing the best cells to meet timing, power, and area requirements.

### 6. `[INFO]: Run Directory: /openlane/designs/picorv32a/runs/RUN_2024.08.25_18.36.22`
- **Explanation**: The directory where all the files and results of this specific run will be stored is `/openlane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43`. This directory is automatically created with a timestamp (`2024.08.25_18.46.43`) to differentiate between different runs.

### 7. `[WARNING]: SYNTH_MAX_FANOUT is now deprecated; use MAX_FANOUT_CONSTRAINT instead.`
- **Explanation**: This warning indicates that the `SYNTH_MAX_FANOUT` parameter is no longer in use. Users are recommended to use the `MAX_FANOUT_CONSTRAINT` parameter instead for controlling the maximum fanout during synthesis.

### 8. `[INFO]: Saving runtime environment...`
- **Explanation**: OpenLane saves the current runtime environment, including all relevant settings and environment variables. This helps in ensuring reproducibility and debugging if needed.

### 9. `[INFO]: Preparing LEF files for the nom corner...`
- **Explanation**: LEF (Library Exchange Format) files are being prepared for the "nom" (nominal) corner. The "nom" corner represents typical process, voltage, and temperature conditions. LEF files contain information about the physical layout of the cells.

### 10. `[INFO]: Preparing LEF files for the min corner...`
- **Explanation**: LEF files are also being prepared for the "min" corner, which represents the slowest or least favorable process, voltage, and temperature conditions. This is important for ensuring the design meets timing and functionality under worst-case scenarios.

### 11. `[INFO]: Preparing LEF files for the max corner...`
- **Explanation**: Similarly, LEF files are prepared for the "max" corner, representing the fastest or most favorable conditions. This helps in verifying that the design does not violate timing or other constraints under best-case scenarios.

### 12. `[WARNING]: PNR_SDC_FILE is not set. It is recommended to write a custom SDC file for the design. Defaulting to BASE_SDC_FILE`
- **Explanation**: This warning indicates that the `PNR_SDC_FILE` (which specifies timing constraints for Place and Route) is not set. OpenLane will default to using the `BASE_SDC_FILE`, but it is recommended to create a custom SDC file tailored to the specific design to ensure better timing optimization during the Place and Route phase.

### 14. `[WARNING]: SIGNOFF_SDC_FILE is not set. It is recommended to write a custom SDC file for the design. Defaulting to BASE_SDC_FILE`
- **Explanation**: Similar to the previous warning, this message indicates that the `SIGNOFF_SDC_FILE` (which is used for final timing sign-off) is not set. Again, OpenLane defaults to the `BASE_SDC_FILE`, but using a custom SDC file is recommended for accurate final timing verification.

---

# RTL2GDS Flow

## 1. Synthesis
Runs `yosys` synthesis on the current design as well as `OpenSTA` timing analysis on the generated netlist. The logs are produced under `/<run_path>/logs/synthesis/`, the timing reports are under `/<run_path>/reports/synthesis/`, and the synthesized netlist under `/<run_path>/results/synthesis/`.
```bash
run_synthesis
```
<img src="images/Day1/Run_Synthesis_Tcl.png" alt="Run_Synthesis_Tcl" width="100%"/>

Open another Terminal tab/window to analyse the synthesis report.

```bash
# Replace `<run_path>` with your directory path
# Example: ~/OpenLane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43
cd <run_path>/reports/synthesis/

# List all files
ll
```
### Synthesis Report: 

<img src="images/Day1/Synthesis_Directory.png" alt="Synthesis_Directory" width="100%"/>

After running the `run_synthesis` command in OpenLane, several report files are generated to provide detailed information about the synthesis process, including area usage, statistics, and specific checks. Here's an explanation of each of these report files:

#### 1. `1-synthesis.AREA_0.chk.rpt`
This file is a check report (`chk.rpt`) related to the area estimation during synthesis. The report typically includes checks and validations performed to ensure that the area usage (in terms of cell count and overall footprint) meets the design requirements or constraints. It may contain warnings or errors if any area-related issues are detected, such as exceeding the area budget.

#### 2. `1-synthesis_pre.stat`
This file contains pre-synthesis statistics. This report captures the state of the design before the synthesis process begins, including information about the design's logic, flip-flops, and other elements before they are optimized and mapped to standard cells. This file is useful for comparing the design before and after synthesis to understand the impact of the synthesis process.

#### 3. `1-synthesis.AREA_0.stat.rpt`
This file is a detailed area report generated after synthesis. It includes statistics on the area occupied by the synthesized design, broken down by different categories, such as standard cells, combinational logic, and sequential elements (like flip-flops). The report provides a summary of how much area each part of the design consumes, helping to analyze and optimize area utilization.

#### 4. `1-synthesis_pre_synth.chk.rpt`
This is a check report generated before the actual synthesis begins. It contains checks related to the design's integrity, constraints, and potential issues that could affect synthesis. This report helps in identifying any problems that need to be addressed before running the synthesis, such as constraint violations or design rule checks.

#### 5. `1-synthesis_dff.stat`
This report file focuses on the statistics of the flip-flops (`DFF` stands for D Flip-Flop) used in the design. It provides information on the number and types of flip-flops present in the synthesized design, including details about their distribution and utilization. This report is particularly important for understanding the design's sequential logic and its impact on overall area and timing.

---

These files collectively provide a comprehensive view of the synthesis process, from pre-synthesis conditions to post-synthesis area utilization and flip-flop statistics. They are essential for analyzing the effectiveness of the synthesis, identifying potential issues, and optimizing the design for better performance, area, and power efficiency.

### Flip Flop Ratio
- One of the first tasks after synthesis is to calculate the Flop Ratio. 
- The Flop Ratio is a metric used to evaluate the utilization of flip-flops in your design.
- It is calculated as the ratio of the number of D flip-flops to the total number of cells in the design.
- These details can be found in the generated `1-synthesis.AREA_0.stat.rpt` file.

```bash
# Extract and store the number of cells
num_cells=$(grep -E 'Number of cells:' 1-synthesis.AREA_0.stat.rpt | awk '{print $NF}')

# Extract and store the number of D Flip-Flops
num_dff=$(grep 'sky130_fd_sc_hd__dfxtp_' 1-synthesis.AREA_0.stat.rpt | awk '{print $2}')

# Calculate the Flip-Flop Ratio in percentage
flip_flop_ratio=$(echo "scale=4; $num_dff / $num_cells * 100" | bc)

# Output the results
echo "Number of Cells: $num_cells"
echo "Number of D Flip-Flops: $num_dff"
echo "Flip-Flop Ratio: $flip_flop_ratio%"
```

#### Explanation of the above termainal commands
<details>
    <summary>Expand or Collapse</summary>
```bash
# Extract and store the number of cells
num_cells=$(grep -E 'Number of cells:' 1-synthesis.AREA_0.stat.rpt | awk '{print $NF}')
```

- **`grep -E 'Number of cells:' 1-synthesis.AREA_0.stat.rpt`**: 
  - `grep -E` searches the file `1-synthesis.AREA_0.stat.rpt` for the line containing the text `Number of cells:`.
  - `-E` allows for extended regular expressions, but in this case, it's just matching a simple string.
  
- **`awk '{print $NF}'`**: 
  - `awk` is a text processing tool.
  - `{print $NF}` tells `awk` to print the last field (`NF` stands for "Number of Fields") of the line matched by `grep`.
  - This extracts the number of cells from the line.
  
- **`num_cells=$(...)`**:
  - The result of the `grep` and `awk` commands is stored in the variable `num_cells`.
  - `$(...)` is command substitution, meaning the output of the command inside the parentheses is assigned to `num_cells`.

```bash
# Extract and store the number of D Flip-Flops
num_dff=$(grep 'sky130_fd_sc_hd__dfxtp_' 1-synthesis.AREA_0.stat.rpt | awk '{print $2}')
```

- **`grep 'sky130_fd_sc_hd__dfxtp_' 1-synthesis.AREA_0.stat.rpt`**:
  - `grep` searches the file `1-synthesis.AREA_0.stat.rpt` for the line containing the specific cell name `sky130_fd_sc_hd__dfxtp_`.
  - This cell name represents the D Flip-Flops in the design.

- **`awk '{print $2}'`**:
  - This tells `awk` to print the second field of the matched line.
  - The second field contains the number of D Flip-Flops.

- **`num_dff=$(...)`**:
  - The number of D Flip-Flops is stored in the variable `num_dff`.

```bash
# Calculate the Flip-Flop Ratio in percentage
flip_flop_ratio=$(echo "scale=2; $num_dff / $num_cells * 100" | bc)
```

- **`echo "scale=2; $num_dff / $num_cells * 100"`**:
  - `echo` outputs the string `"scale=2; $num_dff / $num_cells * 100"`.
  - `scale=2` sets the precision to 2 decimal places for the calculation.
  - `$num_dff / $num_cells * 100` calculates the ratio of D Flip-Flops to total cells and multiplies by 100 to get a percentage.

- **`| bc`**:
  - The output of `echo` is piped to `bc`, a command-line calculator that can handle floating-point arithmetic.
  - `bc` evaluates the expression and returns the result.

- **`flip_flop_ratio=$(...)`**:
  - The result of the `bc` calculation is stored in the variable `flip_flop_ratio`.

```bash
# Output the results
echo "Number of Cells: $num_cells"
echo "Number of D Flip-Flops: $num_dff"
echo "Flip-Flop Ratio: $flip_flop_ratio%"
```

- **`echo "Number of Cells: $num_cells"`**:
  - Prints the total number of cells.

- **`echo "Number of D Flip-Flops: $num_dff"`**:
  - Prints the number of D Flip-Flops.

- **`echo "Flip-Flop Ratio: $flip_flop_ratio%"`**:
  - Prints the Flip-Flop Ratio as a percentage.

These lines provide a detailed output of the synthesis report, showing the number of cells, the number of D Flip-Flops, and the calculated Flip-Flop Ratio.
</details>

### Flip Flop Ratio Output
```
Number of Cells: 16558
Number of D Flip-Flops: 1613
Flip-Flop Ratio: 9.7400%
```
<img src="images/Day1/FlipFlop_Ratio.png" alt="FlipFlop_Ratio" width="100%"/>

### Synthesis Results
After running the synthesis process in OpenLane, two key files are typically generated in the `results/synthesis` folder:

```bash
# Replace `<run_path>` with your directory path
# Example: ~/OpenLane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43
cd <run_path>/results/synthesis/

# List all files
ll
```

#### 1. `picorv32a.sdf` (Standard Delay Format File)

**Purpose:**
- The `picorv32a.sdf` file is a **Standard Delay Format (SDF)** file. It contains timing information extracted from the synthesized design, such as delays for gates, interconnects, and setup/hold times for flip-flops.
- SDF files are used in timing simulations to ensure that the synthesized design meets timing constraints.

**Key Contents:**
- **Delays:** Specifies the propagation delay of signals through gates and interconnects. Delays are often specified for different conditions like minimum, typical, and maximum values.
- **Setup/Hold Times:** Defines the setup and hold times for flip-flops and other sequential elements.
- **Timing Checks:** Includes timing checks that validate if the circuit operates correctly under specified timing constraints.

**Usage:**
- This file is used during post-synthesis and post-layout simulations. By back-annotating the delays in the netlist with the information in the SDF file, a more accurate simulation of the circuit's timing behavior can be achieved.
- Tools like ModelSim, VCS, OpenSTA(in our case) or other simulation tools can use the SDF file to simulate the timing of the synthesized design, ensuring that it will function correctly at the specified clock speed in the final implementation.

#### 2. `picorv32a.v` (Gate-Level Netlist)

**Purpose:**
- The `picorv32a.v` file is the **gate-level netlist** in Verilog format. It represents the synthesized version of the design, where high-level RTL (Register Transfer Level) code has been mapped to specific logic gates and standard cells provided by the technology library (in this case, the `sky130_fd_sc_hd` standard cells).

**Key Contents:**
- **Instances of Standard Cells:** The netlist contains instances of logic gates, flip-flops, multiplexers, etc., mapped from the RTL design to the actual cells in the standard cell library.
- **Wires and Nets:** It shows how the cells are connected via wires or nets.
- **Ports:** Input, output, and bidirectional ports of the design, as defined in the original RTL, are maintained in the gate-level netlist.

**Usage:**
- The gate-level netlist is used in post-synthesis simulations and further stages of the design flow, such as place-and-route (PnR).
- It is a crucial file for verifying that the synthesized design behaves as expected and meets the required specifications before proceeding to physical design steps.
- This file is also useful for generating final layouts and for preparing for the tape-out of the design.

### Synthesised Netlist
The ABC has done all the mappings!
```bash
less picorv32a.v
```
<img src="images/Day1/Synthesised_Netlist.png" alt="Synthesised_Netlist" width="100%"/>

To quit the `less` window, press `q`

### OpenSTA Timing Report
After running the synthesis process in OpenLane, the timing reports are generated in `logs/timimg` folder:

```bash
# Replace `<run_path>` with your directory path
# Example: ~/OpenLane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43
cd <run_path>/logs/synthesis/

# List all files
ls

# View `2-sta.log` file as mentioned in the output of `run_synthesis` command
less 2-sta.log
```
To quit the `less` window, press `q`

<img src="images/Day1/STA_Report.png" alt="STA_Report" width="100%"/>

---

## 2. Floor Plan

Next step is to run the floorplan using this command in the `flow.tcl interactive terminal`.
The resulting files are under `/<run_path>/tmp/floorplan/` and `/<run_path>/results/floorplan/`

```bash
run_floorplan
```
<img src="images/Day2/D2_Lab/Run_Floorplan.png" alt="Run_Floorplan" width="100%"/>

### Calculate the Die area

Navigate to the Floorplan `.def` file in the `tmp/floorplan` folder and use the `less` command to view it in **another terminal tab**

```bash
# Replace `<run_path>` with your directory path
# Example: ~/OpenLane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43
cd <run_path>/tmp/floorplan/

# List all files
ls

# View `3-initial_fp.def` file 
less 3-initial_fp.def
```
To quit the `less` window, press `q`

<img src="images/Day2/D2_Lab/Floorplan_DEF_Die_Area.png" alt="Floorplan_DEF_Die_Area" width="100%"/>

According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 692760 - 0 = 692760
```
```math
Die\ height\ in\ unit\ distance = 703480 - 0 = 703480
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{692760}{1000} = 692.760\ Microns
```
```math
Die\ height\ in\ microns = \frac{703480}{1000} = 703.480\ Microns
```
```math
Area\ of\ die\ in\ microns = 692.760 * 703.480 = 487,342.8048\ Square\ Microns
```

### View floorplan in Magic tool

#### 1. Install Magic Tool

```bash
# Change the directory to the user's home directory
cd ~/

# Clone the Magic VLSI tool repository from GitHub into a directory named "magic"
git clone https://github.com/RTimothyEdwards/magic.git

# Install the necessary dependencies for Magic, including Tcl/Tk libraries, Cairo graphics library, X11 development libraries, M4 macro processor, and ncurses library
sudo apt install tcl tk tk-dev tcl-dev libcairo2 libx11-dev m4 libncurses-dev libcairo2-dev

# Change the directory to the newly cloned "magic" directory
cd magic

# Run the configuration script to prepare the build environment for Magic
./configure
```

<img src="images/Day2/D2_Lab/Magic_Config.png" alt="Magic_Config" width="100%"/>

Now that we have the necessary dependencies installed, lets compile and install the magic tool.

```bash
# Compile the Magic VLSI tool using 5 parallel jobs to speed up the build process
make -j5

# Install the compiled Magic VLSI tool on the system
sudo make install
```
To verify Magic's installation, run: 
```bash
which magic

# You should see something like this:
# /usr/local/bin/magic
```
#### 2. **LEF File:** Navigate to `results/tmp` directory
```bash
# Replace `<run_path>` with your directory path
# Example: ~/OpenLane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43
cd <run_path>/tmp/

# List all files
ls
```
You will find 3 `.lef` files:

<img src="images/Day2/D2_Lab/Merged_LEF.png" alt="Merged_LEF" width="100%"/>

The files generated by OpenLane in the `tmp` directory, specifically `merged.max.lef`, `merged.min.lef`, and `merged.nom.lef`, are related to the **LEF (Library Exchange Format)** files used during the physical design process. Here’s what each file represents:

##### 1. **merged.max.lef**
   - **Purpose:** This file contains the merged LEF information for the design at the maximum process corner. 
   - **Details:** The maximum corner refers to the slowest timing scenario (e.g., the highest operating temperature, lowest supply voltage) where delays are expected to be the longest. This file includes information about the cell layouts and any associated timing information specific to this worst-case condition.

##### 2. **merged.min.lef**
   - **Purpose:** This file contains the merged LEF information for the design at the minimum process corner.
   - **Details:** The minimum corner represents the fastest timing scenario (e.g., the lowest operating temperature, highest supply voltage) where delays are expected to be the shortest. It includes layout and timing information tailored to this best-case condition.

##### 3. **merged.nom.lef**
   - **Purpose:** This file contains the merged LEF information for the design at the nominal process corner.
   - **Details:** The nominal corner is the typical operating condition (standard voltage and temperature) that represents the average case for the design. This file includes standard layout and timing information for cells under normal operating conditions.

##### **General Overview of LEF Files:**
- **LEF Files** are used in ASIC design to describe the physical layout of standard cells, macros, and other IP blocks without the detailed GDSII information. They include abstract representations of the cells, along with routing layer information and pin locations.
- **Merging Process:** During the design process, various LEF files (such as standard cell libraries, custom cell libraries, etc.) are merged into a single LEF file for each process corner. This enables the tools to have a unified view of all available components under the specific corner's conditions.

##### **Why Multiple LEF Files?**
- **Process Corners:** Modern VLSI design considers different process corners to ensure that the chip functions correctly under all possible manufacturing variations. These corners account for the worst-case (maximum), best-case (minimum), and typical (nominal) scenarios.
- **Design Reliability:** By generating and analyzing these different LEF files, the design tools can verify that the chip will meet timing, power, and other constraints across all conditions.

We will use the `merged.nom.lef` file for nominal operation.

#### 3. **PDK Tech File**: 

Refer to the [PDK Root Info Section](#3-info-pdk-root-homeparallelsvolare) to know your `PDK_ROOT` Path.

`<tech_file>` path will be `<PDK_ROOT>/libs.tech/magic/sky130A.tech`

#### 4. Open another terminal and navigate to `results/floorplan` directory
```bash
# Replace `<run_path>` with your directory path
# Example: ~/OpenLane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43
cd <run_path>/results/floorplan/

# List all files
ls
```
<img src="images/Day2/D2_Lab/Floorplan_Results_DEF.png" alt="Floorplan_Results_DEF" width="100%"/>


#### 5. Run Magic tool
```bash
magic -T <tech_file> lef read ../../tmp/merged.nom.lef def read picorv32a.def &

# Start the Magic VLSI tool using the specified technology file
magic -T <tech_file> \
#Eg: magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech \

# Load the merged nominal LEF file (merged.nom.lef) that describes the layout of cells at the nominal process corner
lef read ../../tmp/merged.nom.lef \

# Read the DEF (Design Exchange Format) file for the "picorv32a" design, which contains the placement and routing information
def read picorv32a.def &

# The '&' at the end runs the command in the background, allowing you to continue using the terminal

# Full command Example:
# magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32a.def &
```
<img src="images/Day2/D2_Lab/Floorplan_Magic_Window.png" alt="Floorplan_Magic_Window" width="100%"/><img src="images/Day2/D2_Lab/Floorplan_Magic_Tkcon_Window.png" alt="Floorplan_Magic_Tkcon_Window" width="100%"/>

#### 6. Check Floorplan Settings:
- Equidistant IO Port Pin Placement

<img src="images/Day2/D2_Lab/Equidistant_Pin_Placement.png" alt="Equidistant_Pin_Placement" width="100%"/>

- Metal Layer of Horizontal & Vertical IO Ports should be same as set in `run_path/config.tcl` file.
  - Select the port pin using `s` letter and type `what` in the **tkcon console window**
<img src="images/Day2/D2_Lab/Horizontal_Port_Pins.png" alt="Horizontal_Port_Pins" width="100%"/>
<img src="images/Day2/D2_Lab/Vertical_Port_Pins.png" alt="Vertical_Port_Pins" width="100%"/>

- Standard Cells at Origin (Bottom Left Corner)
<img src="images/Day2/D2_Lab/Standard_Cell_Floorplan.png" alt="Standard_Cell_Floorplan" width="100%"/>

- Decap Cells near IO Port Pins & Diagonally Equidistant Tap cells
<img src="images/Day2/D2_Lab/Decap_Tap_Cells_Floorplan.png" alt="Decap_Tap_Cells_Floorplan" width="100%"/>

6. Exit both windows

## 3. Placement

Run design congestion aware global placement using OpenLANE flow and generate necessary outputs.
**Navigate back to the terminal tab, where the `flow.tcl` interactive console in running**
```bash
# Congestion aware placement by default
run_placement
```
<img src="images/Day2/D2_Lab/Run_Placement.png" alt="Run_Placement" width="100%"/>

### View Placement in Magic Tool
#### 1. Navigate to Placement Results directory
```bash
# Replace `<run_path>` with your directory path
# Example: ~/OpenLane/designs/picorv32a/runs/RUN_2024.08.25_18.46.43
cd <run_path>/results/placement

# List all files
ls
```
#### 2. Run Magic tool
```bash
magic -T <tech_file> lef read ../../tmp/merged.nom.lef def read picorv32a.def &

# Start the Magic VLSI tool using the specified technology file
magic -T <tech_file> \
#Eg: magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech \

# Load the merged nominal LEF file (merged.nom.lef) that describes the layout of cells at the nominal process corner
lef read ../../tmp/merged.nom.lef \

# Read the DEF (Design Exchange Format) file for the "picorv32a" design, which contains the placement and routing information
def read picorv32a.def &

# The '&' at the end runs the command in the background, allowing you to continue using the terminal

# Full command Example:
# magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32a.def &
```
<img src="images/Day2/D2_Lab/Placement_Magic_Window.png" alt="Placement_Magic_Window" width="100%"/>

3. Check by Zooming in whether standard cells appear or not.

<img src="images/Day2/D2_Lab/Placement_Standard_Cells.png" alt="Placement_Standard_Cells" width="100%"/>

# Custom Std Cell Design

 Design standard library cell using Magic and perform timing characterization using NGSpice Tool.

## 1. Clone custom inverter standard cell design from github repository

**Open a new Terminal Tab**
```bash
# Change the directory to the "OpenLane" directory in the user's home directory
cd ~/OpenLane

# Clone the "vsdstdcelldesign" repository from GitHub, which contains standard cell design examples and resources
git clone https://github.com/nickson-jose/vsdstdcelldesign.git

# Change the directory to the newly cloned "vsdstdcelldesign" directory
cd vsdstdcelldesign/

# List all files and directories in the current directory in a detailed format
ll
```

<img src="images/Day3/D3_Lab/Clone_VSD_Inv_Git.png" alt="Clone_VSD_Inv_Git" width="100%"/>

## 2. Load Std Cell in Magic
```bash
# Command to open custom inverter layout in magic
magic -T <tech_file> sky130_inv.mag &
```

<img src="images/Day3/D3_Lab/Custom_Inv_Magic.png" alt="Custom_Inv_Magic" width="100%"/>

## 3. Explore & Verify Std Cell
1. Identify NMOS
  <img src="images/Day3/D3_Lab/Custom_Inv_NMOS.png" alt="Custom_Inv_NMOS" width="100%"/>
2. Identify PMOS
  <img src="images/Day3/D3_Lab/Custom_Inv_PMOS.png" alt="Custom_Inv_PMOS" width="100%"/>
3. Verify Output Port "Y" Connectivity to PMOS & NMOS Drain
  <img src="images/Day3/D3_Lab/Custom_Inv_Y_Connection.png" alt="Custom_Inv_Y_Connection" width="100%"/>
4. Verify PMOS Source connectivity to VPWR
  <img src="images/Day3/D3_Lab/Custom_Inv_VPWR_Connection.png" alt="Custom_Inv_VPWR_Connection" width="100%"/>
5. Verify NMOS Source connectivity to VGND
  <img src="images/Day3/D3_Lab/Custom_Inv_VGND_Connection.png" alt="Custom_Inv_VGND_Connection" width="100%"/>
6. Verify Grid Unit 
- Toggle Grid using the single hotkey `g` and then zoom in (using `z`) to view the grid boxes.
- Selct the Grid box and get the dimensions by typing `box` in the tkcon window.
  <img src="images/Day3/D3_Lab/Custom_Inv_Grid_Unit.png" alt="Custom_Inv_Grid_Unit" width="100%"/>
- Grid Unit is `0.010 Microns`

## 4. SPICE Extraction of Custom Std Cell Design
Run the following commands in the Magic tkcon window
```bash
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```
<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Extraction.png" alt="Custom_Inv_SPICE_Extraction" width="100%"/>

## 5. View extracted SPICE Simulation File
### Extracted SPICE File
<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Extracted.png" alt="Custom_Inv_SPICE_Extracted" width="100%"/>

### Edit the SPICE File
1. Edit the scale to grid unit
2. Include custom inverter libraries for our std cell
3. Change the PMOS & NMOS to the included library names and sub-circuit names
4. Add VDD & VSS for Simulation
5. Define the Input Pulse parameters
6. Increase Load capacitance to reduce output spikes
7. Add the Transient Analysis settings

<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Edited.png" alt="Custom_Inv_SPICE_Edited" width="100%"/>

## 6. Install NGSpice Tool for simulation
```bash
# Install the NGSpice circuit simulator using the system's package manager (apt)
sudo apt install ngspice

# Check the installation path of the 'ngspice' executable
which ngspice
```
<img src="images/Day3/D3_Lab/NGSpice_Installation.png" alt="NGSpice_Installation" width="100%"/>

## 7. Run SPICE Simulation using NGSpice
### Run NGSpice tool
```bash
ngspice sky130_inv.spice
```
<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Run.png" alt="Custom_Inv_SPICE_Run" width="100%"/>

### Plot Input and Output Waveform vs Time
The terminal prompt will change for NGSpice tool. Represented like this: `ngspice 1 -> `

```bash
plot y vs time a
```
A new window will open.
<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Sim.png" alt="Custom_Inv_SPICE_Sim" width="100%"/>
<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Graph.png" alt="Custom_Inv_SPICE_Graph" width="100%"/>

## 8. SPICE Simulation Analysis
We need to calcluate the following:
1. Rise transition time calculation
2. Fall transition time calculation
3. Rise Cell Delay Calculation
4. Fall Cell Delay Calculation

### Rise transition time calculation
```math
Rise\ transition\ time = Time\ taken\ for\ output\ to\ rise\ to\ 80\% - Time\ taken\ for\ output\ to\ rise\ to\ 100\%
```
```math
100\%\ of\ 3.3V\ output = 660\ mV
```
```math
80\%\ of\ 3.3V\ output = 2.64\ V
```

Output Rise till 100%

<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Rise_20.png" alt="Custom_Inv_SPICE_Rise_20" width="100%"/>

Output Rise till 80%

<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Rise_80.png" alt="Custom_Inv_SPICE_Rise_80" width="100%"/>

```math
Rise\ transition\ time = 2.23895 - 2.17938 = 0.05957\ ns = 59.57\ ps
```
---
### Fall transition time calculation
```math
Fall\ transition\ time = Time\ taken\ for\ output\ to\ fall\ to\ 100\% - Time\ taken\ for\ output\ to\ fall\ to\ 80\%
```
```math
100\%\ of\ 3.3V\ output = 660\ mV
```
```math
80\%\ of\ 3.3V\ output = 2.64\ V
```

Output Fall till 100%

<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Fall_20.png" alt="Custom_Inv_SPICE_Fall_20" width="100%"/>

Output Fall till 80%

<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Fall_80.png" alt="Custom_Inv_SPICE_Fall_80" width="100%"/>

```math
Fall\ transition\ time = 4.09305 - 4.05025 = 0.0428\ ns = 42.8\ ps
```
---
### Rise Cell Delay Calculation
```math
Rise\ Cell\ Delay = Time\ taken\ for\ output\ to\ rise\ to\ 100\% - Time\ taken\ for\ input\ to\ fall\ to\ 100\%
```
```math
100\%\ of\ 3.3\ V = 1.65\ V
```
<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Rise_Delay.png" alt="Custom_Inv_SPICE_Rise_Delay" width="100%"/>

```math
Rise\ Cell\ Delay = 2.20702 - 2.15041 = 0.05661\ ns = 56.61\ ps
```
---
### Fall Cell Delay Calculation
```math
Fall\ Cell\ Delay = Time\ taken\ for\ output\ to\ fall\ to\ 100\% - Time\ taken\ for\ input\ to\ rise\ to\ 100\%
```
```math
100\%\ of\ 3.3\ V = 1.65\ V
```
<img src="images/Day3/D3_Lab/Custom_Inv_SPICE_Fall_Delay.png" alt="Custom_Inv_SPICE_Fall_Delay" width="100%"/>

```math
Fall\ Cell\ Delay = 4.07504 - 4.04992 = 0.02512\ ns = 25.12\ ps
```
---

## 9. Check DRC Violation of Custom Std cell
Lets move back to the magic window.

Conditions to be verified before moving forward with custom designed cell layout:
* **Condition 1**: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
* **Condition 2**: Width of the standard cell should be odd multiples of the horizontal track pitch.
* **Condition 3**: Height of the standard cell should be even multiples of the vertical track pitch.

### Condition 1
The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.

#### What are Tracks?
<details>
  <summary>
  Expand or Collapse
  </summary>
In the context of the Sky130A process technology, "tracks" refer to the predefined grid lines on which standard cells, routing wires, and vias are aligned during the physical design of an integrated circuit (IC). Tracks are crucial in defining the placement and routing resources available for designing circuits. 

##### **Understanding Tracks in Sky130A:**

1. **Track Grid:**
   - The track grid is a virtual grid overlaid on each metal layer of the chip. The grid spacing is defined by the technology and is typically aligned with the pitches of the metal layers.
   - Tracks are used to ensure that routing is consistent and follows the design rules specific to the process technology (Sky130A in this case).

2. **Horizontal and Vertical Tracks:**
   - **Horizontal Tracks:** Typically align with horizontal routing on specific metal layers.
   - **Vertical Tracks:** Typically align with vertical routing on specific metal layers.
   - The orientation and spacing of these tracks are designed to optimize routing density and manufacturability.

3. **Usage in Standard Cell Placement:**
   - Standard cells are placed such that their pins align with these tracks, which simplifies routing and ensures that the design adheres to the technology’s design rules.
   - The height of standard cells is usually an integer multiple of the vertical track pitch, ensuring they align perfectly with the grid.

4. **Routing Tracks:**
   - Routing tools use the track information to route signal nets between different components on the chip. By adhering to the tracks, routing tools can avoid violations of design rules and optimize the layout for performance and manufacturability.

5. **Technology File (LEF/DEF):**
   - In the Sky130A process, the tracks are defined in the technology files, such as LEF (Library Exchange Format) files. These files include information about the metal layers, track pitch, and other physical constraints.

6. **Example in Sky130A:**
   - For example, in the Sky130A process, the minimum metal pitch might be 0.23 µm, and the track pitch would be derived from this, defining where wires and vias can be placed. The tracks ensure that the routing is efficient and meets the process rules.

##### **Importance of Tracks:**
- **Design Rule Compliance:** Tracks help in ensuring that the layout adheres to the design rules set by the Sky130A process technology, such as spacing between wires and alignment with the grid.
- **Optimization:** Proper use of tracks allows for efficient use of the chip area, reducing the overall size of the chip and optimizing performance.
- **Manufacturability:** Aligning cells and routing to tracks ensures that the design can be manufactured reliably.
</details>

#### Find out the track width of Sky130A Process Technology
```bash
less <PDK_ROOT>/libs.tech/openlane/sky130_fd_sc_hd/tracks.info
```
<img src="images/Day4/D4_Lab/SKY130A_Tracks_Info.png" alt="SKY130A_Tracks_Info" width="100%"/>


The `tracks.info` file in the Sky130A Process Design Kit (PDK) provides information about the track spacing and alignment for different metal layers and the local interconnect (LI1) layer. This information is used in the physical design process to guide the placement of standard cells and the routing of wires.

**General Format:**
- Each line follows the format:
  ```
  <layer> <orientation> <offset> <pitch>
  ```
  where:
  - `<layer>`: The name of the layer (e.g., `li1`, `met1`, etc.).
  - `<orientation>`: The orientation of the tracks (`X` for horizontal, `Y` for vertical).
  - `<offset>`: The starting position of the first track from the origin (0,0) in micrometers (µm).
  - `<pitch>`: The distance between consecutive tracks in micrometers (µm).

1. **`li1 X 0.23 0.46`**
   - **Layer:** `li1` (Local Interconnect 1)
   - **Orientation:** `X` (Horizontal tracks)
   - **Offset:** `0.23 µm` (The first track is offset by 0.23 µm from the origin)
   - **Pitch:** `0.46 µm` (The horizontal tracks are spaced 0.46 µm apart)

2. **`met1 Y 0.17 0.34`**
   - **Layer:** `met1` (Metal 1)
   - **Orientation:** `Y` (Vertical tracks)
   - **Offset:** `0.17 µm`
   - **Pitch:** `0.34 µm` (The vertical tracks are spaced 0.34 µm apart)

**Key Points:**
- **Track Alignment:** The `offset` value determines where the first track begins on the grid. Ensuring cells and wires align with this grid is crucial for routing efficiency and design rule compliance.
- **Track Pitch:** The `pitch` is critical as it defines the spacing between tracks. Larger pitches allow for thicker wires or reduced resistance but reduce routing density. Smaller pitches increase routing density but may introduce challenges like increased capacitance and crosstalk.
- **Layer Specificity:** Each layer has its own track configuration, optimized for its specific purpose within the chip's routing hierarchy.

This `tracks.info` file is vital for the place-and-route tools to understand the layout grid, ensuring that wires and vias are placed correctly and that the final design adheres to the manufacturing rules of the Sky130A process.

#### Converge/Allign Magic Grid with SKY130A Tracks Info
Set the grid in the **Magic Tkcon Window**
```tcl
# Display the help information for the 'grid' command in Magic.
# This provides details on how to use the grid command to set up the grid spacing.
help grid

# Set the grid spacing in the Magic layout editor:
#  - First value (0.46um): Horizontal grid spacing (X-direction) for routing.
#  - Second value (0.34um): Vertical grid spacing (Y-direction) for routing.
#  - Third value (0.23um): Horizontal grid origin offset (X-direction).
#  - Fourth value (0.17um): Vertical grid origin offset (Y-direction).
# These settings align the grid with the specified track spacing for the current process technology.
grid 0.46um 0.34um 0.23um 0.17um
```
<img src="images/Day4/D4_Lab/Custom_Inv_Magic_Grid_Converge.png" alt="Custom_Inv_Magic_Grid_Converge" width="100%"/>

Press `q` in the terminal to exit `less` window

#### Condition 1 Verified

<img src="images/Day4/D4_Lab/Custom_Inv_Magic_Grid_Intersection_Ports.png" alt="Custom_Inv_Magic_Grid_Intersection_Ports" width="100%"/>

### Condition 2
Width of the standard cell should be odd multiples of the horizontal track pitch.

- The inner white boundary defines the PnR Boundary for the standard cell 
- Draw a box 
- and type `box` in the tkcon window
- it expands to 3 (odd) grid boxes.

```math
Horizontal\ track\ pitch = 0.46\ um
```

```math
Width\ of\ standard\ cell = 1.38\ um = 0.46 * 3
```

<img src="images/Day4/D4_Lab/Custom_Inv_Magic_Width.png" alt="Custom_Inv_Magic_Width" width="100%"/>

### Condition 3
Height of the standard cell should be even multiples of the horizontal track pitch.

The inner white boundary defines the PnR Boundary for the standard cell and it expands to 8 (even) grid boxes.

```math
Vertical\ track\ pitch = 0.34\ um
```
```math
Height\ of\ standard\ cell = 2.72\ um = 0.34 * 8
```

<img src="images/Day4/D4_Lab/Custom_Inv_Magic_Height.png" alt="Custom_Inv_Magic_Height" width="100%"/>

## 10. Rename Magic File
Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name
```tcl
# Command to save as
save sky130_vsdinv.mag
```

Command for the terminal to open the newly saved layout

```bash
# Verify genration of the new `sky130_vsdinv.mag` file
ls

# Command to open custom inverter cell layout in magic
magic -T <tech_file> sky130_vsdinv.mag &
```

<img src="images/Day4/D4_Lab/VSD_Inv_Magic.png" alt="VSD_Inv_Magic" width="100%"/>

## 11. Generate LEF File for Custom Std Cell using Magic
Command for tkcon window to generate the lef file with the same base file name for the custom inverter cell.

```tcl
lef write
```
<img src="images/Day4/D4_Lab/VSD_Inv_LEF_Generation.png" alt="VSD_Inv_LEF_Generation" width="100%"/>

View LEF File in terminal
```bash
less sky130_vsdinv.lef
```
<img src="images/Day4/D4_Lab/VSD_Inv_LEF_View.png" alt="VSD_Inv_LEF_View" width="100%"/>

**Press `q` to exit less window**

## 12. Add Custom Cell to Your Design folder
1. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

```bash
# Copy lef file
cp sky130_vsdinv.lef ~/OpenLane/designs/picorv32a/src/

# List and check whether it's copied
ll ~/OpenLane/designs/picorv32a/src

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/OpenLane/designs/picorv32a/src/

# List and check whether it's copied
ll ~/OpenLane/designs/picorv32a/src
```

  <img src="images/Day4/D4_Lab/VSD_Inv_LEF_LIB.png" alt="VSD_Inv_LEF_LIB" width="100%"/>

2. Edit `picorv32a/config.tcl` to change lib file and add the new extra lef into the openlane flow.

Add these lines:
```tcl
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

  <img src="images/Day4/D4_Lab/VSD_Inv_Config_Tcl.png" alt="VSD_Inv_Config_Tcl" width="100%"/>


# Re-Run OpenLane flow for custom cell design

**Now that a new LEF File for our Custom Cell design has been added, we need to restart our RTL to GDF Flow to genrate the new netlist and so on.**

## 1. Exit & Rerun the current flow.

In the terminal tab, where the `flow.tcl` was running:
```bash
# Exit flow.tcl
exit
# The terminal prompt should now change from `%` to the `Openlane Container` environment.

./flow.tcl -interactive
# Terminal Environment should change to Flow.tcl represented by `%`
```


## 2. Prep Design with additional LEF Files
```bash
# Load the required OpenLane version 0.9 package to access OpenLane commands and features.
package require openlane 0.9

# Prepare the design environment for the specified design (picorv32a in this case).
# The '-tag' option is used to specify a unique run directory tag that identifies this particular run.
# The '-overwrite' option allows overwriting any existing run directory with the same tag.
# Example: prep -design picorv32a -tag RUN_2024.08.25_18.46.43 -overwrite
prep -design picorv32a -tag <RUN_DIR_TAG> -overwrite

# Include additional commands to integrate newly added custom cell LEF files into the OpenLane flow.
# The 'glob' command is used to get a list of all LEF files in the 'src' directory of the design.
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]

# The 'add_lefs' command adds the specified LEF files to the design flow, ensuring they are included in subsequent steps.
add_lefs -src $lefs

# Now that the design is prepared and custom LEF files are included, we can proceed to run the synthesis step.
# The 'run_synthesis' command will execute the Yosys synthesis process for the prepared design.
run_synthesis
```
<img src="images/Day4/D4_Lab/Custom_Inv_Prep_Synthesis.png" alt="Custom_Inv_Prep_Synthesis" width="100%"/>

## 3. Verify LEF Merge for custom cell
Check the `<run_path>/tmp/merged.nom.lef` file to confirm whether it contains a new macro for our `sky130_vsdinv` inverter.

<img src="images/Day4/D4_Lab/Custom_Inv_Merged_LEF.png" alt="Custom_Inv_Merged_LEF" width="100%"/>

## 4. Post-Synthesis Timing Analysis
We need to ensure that we dont have any slack violations after including the new custom inverter cell `sky130_vsdinv`

Analyse `<run_path>/logs/synthesis/2-sta.log` as mentioned in the output of `run_synthesis` step of Openflow. 

**Our hold and setup slack should be possitive or 0**

<img src="images/Day4/D4_Lab/Custom_Inv_Post_Synthesis_STA.png" alt="Custom_Inv_Post_Synthesis_STA" width="100%"/>

## 5. Floorplan with Custom Cell
As per [OpenLane Floorplan Commands Docs](https://armleo-openlane.readthedocs.io/en/latest/docs/source/openlane_commands.html#floorplan-commands),
The `run_floorplan` command involves the following:

1. `init_floorplan` : Runs floorplanning on the processed design using the openroad app. The resulting file is under `/<run_path>/tmp/floorplan/`

2. `place_io` : Runs io placement on the design processed using the openroad app. The resulting file is under `/<run_path>/tmp/floorplan/`

3. `tap_decap_or` : Runs tap/decap placement on the design processed using the openroad app. 
The resulting file is under `/<run_path>/tmp/floorplan/`

4. `gen_pdn` : Runs basic power grid generation on the processed design using the openroad app. The resulting file is under `/<run_path>/tmp/pdn`

But we dont need the 4th step of PDN Generation as of now, so we will run only the first 3 steps individually.

```bash
init_floorplan
place_io
tap_decap_or
```
<img src="images/Day4/D4_Lab/Custom_Inv_Floorplan.png" alt="Custom_Inv_Floorplan" width="100%"/>

## 6. Placement with custom cell
Global placement followed by Detailed Placement
```bash
run_placement
```
<img src="images/Day4/D4_Lab/Custom_Inv_Run_Placement.png" alt="Custom_Inv_Run_Placement" width="100%"/>

## 7. Verify Placement of Custom Cell in Magic
In another terminal tab, run the following commands to view the placed design in Magic.
```bash
cd <run_path>/results/placement

magic -T <tech_file> lef read ../../tmp/merged.nom.lef def read picorv32a.def &
# Example:
# magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32a.def &
```

<img src="images/Day4/D4_Lab/Custom_Inv_Placement.png" alt="Custom_Inv_Placement" width="100%"/>

Locate the Custom VSD Inverter Cell, somewhere near the white box highlited in the picture.

<img src="images/Day4/D4_Lab/Custom_Inv_Placement_Global.png" alt="Custom_Inv_Placement_Global" width="100%"/>

Zoom in to the box and locate the cell

<img src="images/Day4/D4_Lab/Custom_Inv_Placement_Located.png" alt="Custom_Inv_Placement_Located" width="100%"/>

Command for tkcon window to view internal layers of cells
```bash
# Command to view internal connectivity layers
expand
```

<img src="images/Day4/D4_Lab/Custom_Inv_Placement_Internal_Layers.png" alt="Custom_Inv_Placement_Internal_Layers" width="100%"/>

## 8. Clock Tree Synthesis (CTS)
With placement done we are now ready to run CTS in the OpenLane Flow
```bash
run_cts
```
<img src="images/Day4/D4_Lab/Custom_Inv_CTS_Run.png" alt="Custom_Inv_CTS_Run" width="100%"/>

## 9. Post-CTS OpenRoad Timing Analysis

We need to again check for any slack violations in the STA Analysis done after CTS, log for which will be sotred in the `<run_path>/logs/cts/15-cts_sta.log` file as mentioned in the last line of the output of `run_cts`

The SLACK should be greater than or equal to 0 == SLACK MET Condition

<img src="images/Day4/D4_Lab/Custom_Inv_Post_CTS_STA.png" alt="Custom_Inv_Post_CTS_STA" width="100%"/>

## 10. PDN Generation
I was encountering random errors at this stage so had to rerun from scratch the entire flow.
Here's a summary of all the commands:

```bash
cd ~/OpenLane
make mount
```

Now we enter the Openlane container environment

```bash
./flow.tcl -interactive
```
Now we have entered the Openlane Flow Tcl Interactive Environment

```bash
package require openlane 0.9

prep -design picorv32a

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

run_synthesis

init_floorplan
place_io
tap_decap_or

run_placement

run_cts

run_power_grid_generation

gen_pdn
```
<img src="images/Day5/D5_Lab/Custom_Inv_PDN_Run.png" alt="Custom_Inv_PDN_Run" width="100%"/>

Once the PDN is generated, you can view it in Magic
In another terminal tab, run the following commands to view the design with PDN in Magic.

Note that `<run_path>` has now changed.
```bash
cd <run_path>/results/floorplan

magic -T <tech_file> lef read ../../tmp/merged.nom.lef def read picorv32a.def &
# Example:
# magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32a.def &
```

<img src="images/Day5/D5_Lab/Custom_Inv_PDN_Magic.png" alt="Custom_Inv_PDN_Magic" width="100%"/>

## 11. Routing
We will use **Triton Route**

```bash
run_routing
```
<img src="images/Day5/D5_Lab/Custom_Inv_Routing_DRC_Error.png" alt="Custom_Inv_Routing_DRC_Error" width="100%"/>

Got an error: `[ERROR DRT-0085] Valid access pattern combination not found for _24236_`
After checking the netlist `_24236_ is our custom cell`
The error code `DRT-0085` tells us that the error was encountered during Detailed Routing (DRT) phase and the router is not able to figure out how it can access all the pins of the instance.

This seems most likely a DRC issue we overlooked earlier.

So lets analyse our Custom VSD Inverter Magic File again for DRC.

## 12. DRC check for Custom Cell
Open another terminal tab and run the following commands:
```bash
cd ~/OpenLane/vsdstdcelldesign

magic -T <tech_file> sky130_vsdinv.mag &
# Example : 
# magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech sky130_vsdinv.mag &
```
In the tkcon magic window,
```bash
drc check
drc why
```
There are 4 DRC Errors regarding sizing of nwell and transistor width, highlighted with white patches.

<img src="images/Day5/D5_Lab/Custom_Inv_DRC_Error.png" alt="Custom_Inv_DRC_Error" width="100%"/>

After fixing them, we will save it in a new mag file and generate the new lef

Tkcon window:
```bash
save sky130_vsdinv_drc.mag
lef write
```
<img src="images/Day5/D5_Lab/Custom_Inv_Routing_DRC_Solved.png" alt="Custom_Inv_Routing_DRC_Solved" width="100%"/>

Copy the new LEF to our picorv32a design source folder.
Terminal Window:
```bash
cp sky130_vsdinv.lef ~/OpenLane/designs/picorv32a/src/
```

## 13. Rerun after solving DRC
Now we again have to rerun the entire flow to include the new LEF in the netlist.

New Terminal:
```bash
cd ~/OpenLane
make mount
```

Now we enter the Openlane container environment

```bash
./flow.tcl -interactive
```
Now we have entered the Openlane Flow Tcl Interactive Environment

```bash
package require openlane 0.9

prep -design picorv32a

set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

run_synthesis

init_floorplan
place_io
tap_decap_or

run_placement

run_cts

run_power_grid_generation

gen_pdn

run_routing
```

**And its done!**

<img src="images/Day5/D5_Lab/Custom_Inv_Routed_1.png" alt="Custom_Inv_Routed_1" width="100%"/><img src="images/Day5/D5_Lab/Custom_Inv_Routed_2.png" alt="Custom_Inv_Routed_2" width="100%"/>

## 14. View the Final Layout in Magic

Note that `<run_path>` has now changed.
```bash
cd <run_path>/results/routing

magic -T <tech_file> lef read ../../tmp/merged.nom.lef def read picorv32a.def &
# Example:
# magic -T /home/parallels/.volare/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def read picorv32a.def &
```

<img src="images/Day5/D5_Lab/Custom_Inv_Final_Layout_Magic_1.png" alt="Custom_Inv_Final_Layout_Magic_1" width="100%"/><img src="images/Day5/D5_Lab/Custom_Inv_Final_Layout_Magic_2.png" alt="Custom_Inv_Final_Layout_Magic_2" width="100%"/>

## 15. Post-Route STA Analysis
This can be found in `logs/routing/24-grt_sta.log`

<img src="images/Day5/D5_Lab/Custom_Inv_Post_Route_STA.png" alt="Custom_Inv_Post_Route_STA" width="100%"/>

## 16. Post-Route parasitic extraction using SPEF Extractor

New Terminal: 
Install SPEF Extractor
```bash
# Home Directory
cd ~/

# Install Dependencies
pip install numpy sympy matplotlib

# Clone the SPEF Git Repo
git clone https://github.com/HanyMoussa/SPEF_EXTRACTOR.git

# Change to SPEF directory
cd SPEF_EXTRACTOR

# Install
python3 -m pip install spef-extractor

# Verify Install Location
ls <spef-extractor_installation_path>
# Eg: ls /home/parallels/.local/bin
```
<img src="images/Day5/D5_Lab/Install_SPEF_Extractor_1.png" alt="Install_SPEF_Extractor_1" width="100%"/><img src="images/Day5/D5_Lab/Install_SPEF_Extractor_2.png" alt="Install_SPEF_Extractor_2" width="100%"/>

Note down the installation path.

Extract SPEF, the output SPEF file will be in the same directory as the def file.

```bash
# Extract spef
<spef-extractor_installation_path>/spef_extractor -l <run_path>/tmp/merged.nom.lef -d <run_path>/results/routing/picorv32a.def

# Example:
# /home/parallels/.local/bin/spef_extractor -l /home/parallels/OpenLane/designs/picorv32a/runs/RUN_2024.09.01_20.18.16/tmp/merged.nom.lef -d /home/parallels/OpenLane/designs/picorv32a/runs/RUN_2024.09.01_20.18.16/results/routing/picorv32a.def

# Verify
cd <run_path>/results/routing

ls
```
<img src="images/Day5/D5_Lab/Custom_Inv_SPEF_Extraction.png" alt="Custom_Inv_SPEF_Extraction" width="100%"/>

# Extra: Practice DRC Violations on old Sky130 Tech file.

```bash
cd ~/
git clone https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/blob/main/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests
magic -d XR &
```
tkcon window:
```bash
load poly
```
<img src="images/drc_tests/Poly.png" alt="Poly" width="100%"/>

## 1. [Poly.9](https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html#poly)
<img src="images/drc_tests/Poly9_Rule.png" alt="Poly9_Rule" width="100%"/>
tkcon window:
Poly resistor spacing to poly or spacing (no overlap) to diff/tap = 0.48 microns
```bash
snap int
box
```
Spacing (Height) is 0.21 microns, hence incorrect

Fix in Tech File:


<img src="images/drc_tests/Poly9_Incorrect.png" alt="Poly9_Incorrect" width="100%"/>



# Acknowledgements

* [Kunal Ghosh](https://github.com/kunalg123), Co-founder, VSD Corp. Pvt. Ltd.
* [Nickson P Jose](https://github.com/nickson-jose), Physical Design Engineer, Intel Corporation.
* [R. Timothy Edwards](https://github.com/RTimothyEdwards), Senior Vice President of Analog and Design, efabless Corporation.
