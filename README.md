# Implementation
My implementation utilized this hardware:
- Zybo Z7-20 SoC
- PMOD I2S2
## Function of This Program:
This project implements the I2S protocol to receive audio input, processes it through various FIR filters derived from MATLAB, and then outputs the filtered audio via the same I2S protocol. Timing closure was achieved by pipelining the FIR filter stages.

## Features:
- Real-time filtering
- Supports stereo audio input via I2S protocol
- Configurable 64-tap FIR filter with fixed-point coefficients
- Pipelined architecture for high throughput
- Written in Verilog HDL with comprehensive testbenches

The process begins with building the I2S protocol for the PMOD I2S2 to recieve and transmit data as shown initially in the flowchart. Once the data is being recieved into the FPGA, we direct it to the FIR filter. This filter is also binded to a switch which allows you to specifically select which type of filter is being operated. Finally, the data is exported back to the PMOD I2S2 to play it through the line out port.

## How to setup this project:

Initially, there is two Xilinx IP's used in this project:
- Clock Wizard (For generating MCLK)
- DDS Compiler (For Testing FIR filter)

Clock Wizard was used to generate the master clock for the PMOD I2S2 peripherals. This allowed my system to operate at 22.579 MHz. The sampling rate occupied for this project was 44.1 KHz which was generated through a Clock Divider. 

The DDS compiler was used to generate a input sinusoid with a low frequency of 500 Hz and a high frequency of 5000 Hz. This allowed me to test the effect of the FIR filter on a noisy sinusoid.
