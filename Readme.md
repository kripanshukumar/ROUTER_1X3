# ROUTER 1X3 DESIGN USING MODELSIM, QUARTUS PRIME, AND QUESTASIM

## TABLE OF CONTENTS
* [INTRODUCTION](https://github.com/kripanshukumar/ROUTER_1X3#introduction)
    

## Introduction
This repository serves the purpose of presenting the design of a 1X3 8 bit router. It contains the RTL desing, Simulation and Synthesis using softwares like Modelsim, Quartus prime, and Questasim. The language used for RTL code is Verilog.

## Software Used
To make this project happen a total of 3 softwares are used and are described as follows:

### Modelsim by Mentor Graphics
ModelSim is a multi-language environment by Mentor Graphics, for simulation of hardware description languages such as VHDL, Verilog and SystemC, and includes a built-in C debugger. ModelSim can be used independently, or in conjunction with Intel Quartus Prime, PSIM, Xilinx ISE or Xilinx Vivado. ModelSim eases the process of finding design defects with an intelligently engineered debug environment that efficiently displays design data for analysis and debug of all hardware description languages.

<img src="https://i.redd.it/6741k1f4jyz41.jpg" width=33% height=33%>

### Quartus Prims
Intel Quartus Prime is programmable logic device design software produced by Intel; prior to Intel's acquisition of Altera the tool was called Altera Quartus Prime, earlier Altera Quartus II. The revolutionary Intel® Quartus® Prime Design Software includes everything you need to design for Intel® FPGAs, SoCs, and complex programmable logic device (CPLD) from design entry and synthesis to optimization, verification, and simulation. Dramatically increased capabilities on devices with multi-million logic elements are providing designers with the ideal platform to meet next-generation design opportunities.

<img src="https://www.intel.com/content/dam/docs/us/en/683855/current/dql1496958792382.png" width=50% height=50%>

### Questa Advanced Simulator
The Questa Advanced Simulator is the core simulation and debug engine of the Questa Verification Solution; the comprehensive advanced verification platform capable of reducing the risk of validating complex FPGA and SoC designs. The Questa Advanced simulator supports all design languages and constructs, and either automatically or manually partitions the design to run in parallel while maintaining a single database for debug and coverage.

<img src="https://i.pinimg.com/474x/6f/09/b3/6f09b3cc8f50f47bb63754bc0b577c8b.jpg" width=50% height=50%>

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


## CODE COVERAGE REPORT
Code coverage measures how much of the “design Code” is exercised. This includes the execution of design blocks, Number of Lines, Conditions, FSM, Toggle and Path. The simulator tool will automatically extract the code coverage from the design code.

<img src="images/Code%20Coverage/Code%20Coverage%20Questasim.png" width=100% height=100%>

<img src="images/Code%20Coverage/Code%20Coverage%20Questasim%202.png" width=100% height=100%>
