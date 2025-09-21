# UART Peripheral for Microwatt SoC

This repository adds a **Universal Asynchronous Receiver Transmitter (UART)** 
as a memory-mapped peripheral to the [Microwatt](https://github.com/antonblanchard/microwatt) 
open-source PowerPC softcore.

## Features
- UART Transmitter and Receiver
- Baud Rate Generator
- Memory-mapped Wishbone interface
- FPGA tested on DE1-SoC board
- Compatible with Microwatt SoC

## Repository Layout
- `rtl/` : Verilog source code for UART (TX, RX, Baud)
- `soc/` : VHDL wrapper + Wishbone bus integration
- `sim/` : Testbenches for UART & SoC integration
- `fpga/`: Quartus project files, pin assignments
- `docs/`: Documentation and original project report
- `tests/`: C test programs to run on Microwatt CPU

## Memory Map
| Address | Register      | Description              |
|---------|---------------|--------------------------|
| 0x00    | UART_DATA     | TX write / RX read       |
| 0x04    | UART_STATUS   | TX busy, RX ready, Errs  |
| 0x08    | UART_BAUD     | Baud rate divisor        |
| 0x0C    | UART_CONTROL  | Enable, reset, interrupts|

## How to Run
1. Clone Microwatt repo and this repo inside `soc/`:
   ```sh
   git clone https://github.com/antonblanchard/microwatt
   git clone https://github.com/TMRgit/chipfoundry-uart
