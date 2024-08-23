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
