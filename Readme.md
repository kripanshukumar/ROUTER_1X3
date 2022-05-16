# ROUTER 1X3 DESIGN

## Introduction
This repository serves the purpose of presenting the design of a 1X3 8 bit router. It contains the RTL desing, Simulation and Synthesis using softwares like Modelsim, Quartus prime, and Questasim. The language used for RTL code is Verilog.

## Construct
### FIFO
FIFO stands for First In First Out, it is a memory block in which the data entered first is the one which is taken out. In the router the main task of FIFO is to store the incoming packets from the source and acts as a buffer between source an destination. It also helps to transfer data from source to destination both working at different data transfer rate.

<img src="images/FIFO_SYNTHESIS/Screenshot%202022-05-16%20173621.png" width=100% height=100%>

### SYNCHRONIZER
As the name suggests the synchronizer synchronizes the operation between the FIFO, Register, and FSM. It takes control signals from the FSM and the FIFO block and generates the intermediate signal for sub-blocks. The synchronizer contains internal counter which is used to check the timeout condition. Timeout condition occurs when the FIFO contains atleast one byte and the read enable single in not asserted within the next 30 clock cycles.

<img src="images/SYNC_SYNTHESIS/Screenshot%202022-05-16%20174654.png" width=100% height=100%>

### FSM

FSM stands for FINITE STATE MACHINE, and this FSM contains a total of 8 states and is a Moorey machine. The FSM takes care of producing signals like laf_state, lfd_state, ld_state, detect_address, busy, and uses signals from the destination and internal block for the routing of packets.

<img src="images/FSM_SYNTHESIS/Screenshot%202022-05-16%20173917.png" width=100% height=100%>

### REGISTER

REGISTER block is made up of 4 internal 8 bit register named HEADER_BYTE, FIFO_FULL_STATE_BYTE, INTERNAL_PARITY_BYTE, PACKET_PARITY_BYTE, and combinational block taking input signals from FSM to latch the incoming byte in different register according to the FSM state and FIFO occupancy. This register is very crucial in storing the live byte in the case of fifo full. It also calculates the internal parity along with the incoming data, compares it with the packet parity byte and generates the error signal if the internal parity is not equal to packet parity byte.

<img src="images/REG_SYNTHESIS/Screenshot%202022-05-16%20174353.png" width=100% height=100%>
