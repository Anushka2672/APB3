# FPGA-Based Implementation of AMBA APB3 Master–Slave System

## Project Overview

This project implements an **AMBA APB3 (Advanced Peripheral Bus 3) Master–Slave system using Verilog HDL** on the Digilent Nexys A7-100T FPGA board.

The design consists of an APB3 Master, an Address Decoder, and three peripheral slaves: **UART, FIFO, and PWM**. The APB3 Master controls read and write transactions, while the Address Decoder selects the required peripheral based on the address.

The project is developed using Xilinx Vivado and demonstrates RTL design, FSM-based bus control, peripheral interfacing, simulation, and FPGA hardware implementation.

## Project Objectives

- Implement the AMBA APB3 communication protocol.
- Design an APB3 Master using a finite state machine.
- Develop an Address Decoder for peripheral selection.
- Interface UART, FIFO, and PWM slave peripherals.
- Perform RTL simulation, synthesis, and FPGA hardware testing.
- Understand memory-mapped peripheral communication.

##  System Architecture

The system consists of the following modules:

1. **APB3 Master:** Generates APB control signals and manages read/write transactions.
2. **APB3 Address Decoder:** Decodes the peripheral address and activates the appropriate slave.
3. **UART Slave:** Supports APB-based data access and UART transmission.
4. **FIFO Slave:** Provides First-In, First-Out data buffering.
5. **PWM Slave:** Supports pulse-width modulation control through APB transactions.

## Peripheral Address Map

| Peripheral | Address |
|---|---|
| UART Slave | `0x05` |
| FIFO Slave | `0x20` |
| PWM Slave | `0x30` |

##  APB3 Interface Signals

| Signal | Description |
|---|---|
| `PCLK` | APB clock |
| `PRESETn` | Active-low reset |
| `PSEL` | Peripheral select |
| `PENABLE` | Access phase indicator |
| `PWRITE` | Read/write control |
| `PADDR` | Peripheral address |
| `PWDATA` | Write data |
| `PRDATA` | Read data |
| `PREADY` | Transfer-ready indication |
| `PSLVERR` | Transfer error indication |

##  Hardware and Software Requirements

### Hardware
- Digilent Nexys A7-100T FPGA board
- USB cable for FPGA programming and UART communication

### Software
- Xilinx Vivado
- Verilog HDL
- Vivado Simulator (XSim)
- PuTTY or another serial terminal for UART testing

## Technology Stack

- **HDL:** Verilog
- **Bus Protocol:** AMBA APB3
- **Design Methodology:** RTL Design and FSM
- **FPGA:** Artix-7 XC7A100T
- **Development Tool:** Xilinx Vivado
- **Verification:** RTL Simulation and FPGA Hardware Testing

## Project Structure

```text
APB3-Master-Slave/
├── rtl/
│   ├── apb3_master.v
│   ├── apb3_decoder.v
│   ├── uart_slave.v
│   ├── uart_transmitter.v
│   ├── baud_generator.v
│   ├── fifo_slave.v
│   ├── pwm_slave.v
│   └── top.v
├── constraints/
│   └── nexys_a7.xdc
└── README.md
```

*Adjust the filenames and folders to match the files in your actual repository.*

##  Working Principle

1. The user provides an address and data through the FPGA switches.
2. The upper 8 bits, `SW[15:8]`, represent write data, and the lower 8 bits, `SW[7:0]`, represent the APB address.
3. The APB3 Master detects a new command and begins a transaction.
4. The transaction proceeds through the IDLE, SETUP, and ACCESS states.
5. The Address Decoder selects the UART, FIFO, or PWM slave according to `PADDR`.
6. The selected slave responds to the APB transaction using the appropriate control and data signals.
7. The APB3 Master completes the transaction when the selected slave asserts `PREADY`.

## APB3 Master FSM

The APB3 Master uses three states:

- **IDLE:** Waits for a transaction request.
- **SETUP:** Asserts `PSEL` and prepares the transaction.
- **ACCESS:** Asserts `PENABLE` and waits for `PREADY`.


## 🔮 Future Enhancements

- Add SystemVerilog assertions and functional coverage.
- Expand the system with additional APB-compatible peripherals.

