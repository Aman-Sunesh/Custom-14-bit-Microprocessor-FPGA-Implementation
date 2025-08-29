# Custom 14-bit Microprocessor – FPGA Implementation

A fully custom **14-bit microprocessor** implemented in VHDL and deployed on FPGA hardware.  
This project demonstrates the complete design cycle: from basic simulation models to a fully integrated processor running binary programs with FPGA demonstration.

---

## Key Features

- **Word Size:** 14-bit signed data handling  
- **Instruction Set:** 16 operations (arithmetic, logic, branching, memory, jump, halt)  
- **Registers:** 8 general-purpose registers (R0–R7)  
  - R0 is constant zero (hardwired, cannot be overwritten)  
- **Instruction Memory:** 128 entries  
- **Execution:** One instruction per clock cycle  
- **Overflow Detection:** Enabled for signed arithmetic operations  
- **Display Integration:** Results visualized using seven-segment display controller  
- **FPGA Demonstration:** Binary programs compiled and executed directly on hardware  

---

## Repository Structure

- **Process_Sim/**
  - Early simulation stage for the processor.  
  - Contains the base modules (ALU, Controller, Decoder, PC, Registers, Instruction ROM).  
  - Includes testbenches for verifying the fetch–decode–execute cycle.  
  - Used to confirm correctness of the core datapath and control flow in simulation.

- **Process_MPU/**
  - First integrated processor build.  
  - Combines the datapath and control into a working microprocessor.  
  - Includes FPGA constraint files and hardware-level wiring.  
  - Runs example binary programs to validate correct execution on board.

- **Top_Processor/**
  - Finalized microprocessor design.  
  - Fully integrated with display controller for FPGA demonstration.  
  - Includes program memory, control logic, and hardware synthesis files.  
  - Executes custom binary programs (e.g., arithmetic loops, Fibonacci sequence) end-to-end on FPGA.

- **Report.pdf**
  - Detailed documentation of the design, architecture diagrams, simulation results, and FPGA verification.  

---

## Core Modules

- **Registers.vhd**  
  - 8 × 14-bit registers.  
  - Dual read ports (`Rs1`, `Rs2`) and one write port (`Rd`).  
  - Write occurs only when enabled; R0 is permanently zero.  

- **Decoder.vhd**  
  - Parses 16-bit instruction word.  
  - Extracts opcode, register addresses, and immediate values.  

- **Controller.vhd**  
  - Central control logic ("brain" of the processor).  
  - Directs signals between registers, ALU, and program counter.  
  - Handles branching, jumps, and flow control.  

- **ALU.vhd**  
  - Executes arithmetic and logical operations on 14-bit signed operands.  
  - Supports overflow detection.  

- **PC.vhd**  
  - Program counter with increment, branch, and jump functionality.  

- **Instruction_ROM.vhd**  
  - 128-entry instruction memory.  
  - Stores binary programs for execution.  

- **Display_Controller (black box IP)**  
  - Drives seven-segment displays on FPGA.  
  - Used in final integration to visualize processor outputs.  

- **common.vhd**  
  - Defines the opcode type and instruction formats.  

---

## Tools & Environment

- **Language:** VHDL  
- **FPGA Board:** Xilinx Basys2  
- **Software:** Xilinx ISE Design Suite (ISim for simulation, BitGen for FPGA programming)  

---

## How to Run

1. Clone the repository:  
   ```bash
   git clone https://github.com/Aman-Sunesh/Custom-14-bit-Microprocessor-FPGA-Implementation.git
   cd Custom-14-bit-Microprocessor-FPGA-Implementation
   ```

2. Open the appropriate project (`Process_Sim`, `Process_MPU`, or `Top_Processor`) in Xilinx ISE.

3. Add all `.vhd` files and use the provided `.ucf` constraint files for FPGA pin mapping.

4. Run behavioral simulation with ISim to observe instruction execution.

5. Synthesize the design and generate the `.bit` bitstream.

6. Program the FPGA board and observe processor behavior (register updates, outputs on display).  

---

## Demonstration

- **Simulation**  
  - Verified with programs such as arithmetic operations, loops, and branching.  
  - One clock cycle per instruction confirmed.  
  - Overflow behavior observed during subtraction tests.  

- **Hardware Execution**  
  - Example programs executed directly on FPGA.  
  - Arithmetic sequences and branching operations verified.  
  - Fibonacci sequence successfully implemented, computed iteratively, and halted upon completion.  

---

## License

This repository is shared under the **MIT License**.  
You are welcome to use and adapt the designs for personal or educational projects.

---

## Contact

Developed by **Aman Sunesh**  
- [LinkedIn](https://www.linkedin.com/in/aman-sunesh/)  
- Email: as18181@nyu.edu  

---
