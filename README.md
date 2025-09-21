# UART Peripheral for Microwatt SoC

## Summary
This project adds a **UART peripheral** to the **Microwatt SoC**.  
It provides **serial console support**, debugging, and basic I/O.  
The design includes a **Verilog UART core** (TX, RX, baud generator).  
A **VHDL Wishbone wrapper** integrates the UART with memory-mapped registers.  
Simulation testbenches and **example C programs** demonstrate usage on FPGA and simulation.  

## Features
- Full-duplex UART (TX/RX) with configurable baud rate
- Memory-mapped registers: DATA, STATUS, CONTROL, BAUD
- Wishbone bus interface for Microwatt integration
- Simulation testbenches and FPGA support
- Example C software for testing UART communication





## 1️ Motivation
- Extend **Microwatt** with essential I/O functionality (serial console).  
- Demonstrate **peripheral integration** into an open-source CPU SoC.  
- Provide a **reusable UART IP** block for the open hardware community.  
- Enable **real-time communication** and debugging support for Microwatt applications.  

---

## 2️ Core Features
- Full-duplex UART (independent TX and RX).  
- Baud rate generator (configurable divisor).  
- Memory-mapped control/status registers:  
  - **DATA** (read/write)  
  - **STATUS** (TX busy, RX ready, error flags)  
  - **CONTROL** (enable/reset/interrupt enable)  
  - **BAUD** (divisor configuration)  
- Wishbone bus adapter for Microwatt integration.  
- Testbenches (UART core + SoC integration).  
- Example software programs running on Microwatt.  

---

## 3️ High-Level Block Diagram
        ┌───────────────────┐
        │   Microwatt CPU    │
        │ (Instruction + ALU)│
        └────────▲───────────┘
                 │ Wishbone Bus
                 │
      ┌───────────┴─────────────┐
      │  UART Peripheral         │
      │ (Wrapper + Bus Adapter)  │
      └───────┬─────────┬────────┘
              │         │
        UART TXD   UART RXD
              │
     Baud Rate Generator

---

## 4️ Procedure / Implementation Steps
1. **RTL UART Core**  
   - Verilog TX, RX, and Baud Rate Generator modules.  

2. **Bus Integration**  
   - VHDL wrapper + Wishbone adapter for Microwatt.  
   - Memory-mapped register set (DATA, STATUS, CONTROL, BAUD).  

3. **SoC Integration**  
   - Modify Microwatt SoC top-level to instantiate the UART.  
   - Assign base address (default: `0xC0002000`).  

4. **Simulation & Testbenches**  
   - Verify TX/RX, baud rates, framing, parity, and error handling.  
   - Run SoC testbench with Microwatt executing UART code.  

5. **Software Test**  
   - C test program to send/receive characters:  
     ```c
     uart_putc('H');
     uart_putc('i');
     ```  

6. **FPGA Deployment (optional)**  
   - Synthesize design on DE1-SoC (or other FPGA).  
   - Demonstrate live serial output via UART-to-USB.  

---

## 5️ Expected Outcomes
- A functional UART peripheral integrated into Microwatt.  
- Open-source RTL (Verilog + VHDL wrapper) and bus interface.  
- Simulation waveforms + FPGA demonstration.  
- Example software (C tests) for UART communication.  
- Documentation for reuse by the community.  

---

## 6️ Languages Involved
- **Verilog** → UART core (Transmitter, Receiver, Baud Rate Generator).  
- **VHDL** → Microwatt CPU + UART wrapper / Wishbone adapter.  
- **C** → Test programs running on Microwatt CPU.  
- **Markdown** → Documentation (`README.md`, design notes, block diagrams).  
- *(Optional)* **Shell/Make** → Build automation (compile, simulate, synthesize).  

---


