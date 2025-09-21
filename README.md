# UART Peripheral for Microwatt SoC

This repository provides a **Universal Asynchronous Receiver/Transmitter (UART)** peripheral integrated into the [Microwatt](https://github.com/antonblanchard/microwatt) open-source POWER soft CPU.  

The design adapts an FPGA-based UART implementation (transmitter, receiver, baud rate generator) and connects it to Microwatt’s bus system through a memory-mapped interface. It enables the Microwatt CPU to perform serial I/O, supporting console output, debugging, and communication with external devices.

---

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

## 4️⃣ Procedure / Implementation Steps
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


