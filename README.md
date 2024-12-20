# SFAL-VSD-SoC
<details>
	<summary>Day 0 - Tools Installation </summary>
	
# Day 0 - Tools Installation
## Yosys
```
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys 
$ sudo apt install make (If make is not installed please install it) 
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make 
$ sudo make install
```
<img width="800" alt="yosys" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/yosys_1st_run.png">

## Iverilog
```
$ sudo apt-get install iverilog
```
<img width="800" alt="iverilog" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/iverilog_1st_run.png">

## GTKWave
```
$ sudo apt update
$ sudo apt install gtkwave
```
<img width="800" alt="gtkwave2" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/gtkwave_1st_run.png">

<img width="800" alt="gtkwave1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/screen_gtkwave_1st_run.png">
</details>

<details>
<summary>Day 1 - Introduction to Verilog RTL Design and Synthesis</summary>

# Day 1 - Introduction to Verilog RTL Design and Synthesis
## Introduction to open-source simulator Iverilog

Folder structure of the git clone:
- `lib` - will contain sky130 standard cell library
- `my_lib/verilog_models` - will contain standard cell verilog model
- `verilog_files` -contains the lab experiments source files

<img width="800" alt="intro_iverilog" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/iVerilog_intro.png">


Example of a design good_mux.v 

```
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
  if(sel)
    y <= i1;
  else 
    y <= i0;
end
endmodule
```
Example of a testbench tb_good_mux.v 

```
`timescale 1ns / 1ps
module tb_good_mux;
  // Inputs
  reg i0,i1,sel;
  // Outputs
  wire y;

  // Instantiate the Unit Under Test (UUT)
  good_mux uut (
    .sel(sel),
    .i0(i0),
    .i1(i1),
    .y(y)
  );

initial begin
  $dumpfile("tb_good_mux.vcd");
  $dumpvars(0,tb_good_mux);
  // Initialize Inputs
  sel = 0;
  i0 = 0;
  i1 = 0;
  #300 $finish;
end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```
Command to run the design and testbench
```
$iverilog good_mux.v tb_good_mux.v
```
The output of the iverilog is first an a.out. By running/executing vvp a.out, iverilog dump the vcd file.
...
$vvp a.out
...

<img width="800" alt="lab1-gtkwave" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/iverilog_good_mux.png">


## Introduction to GTKWave
gtkwave will be used to generate the waveforms and display in visual format.

Command to view the vcd file in gtkwave 
```
$gtkwave tb_good_mux.vcd
```
The waveform in gtwave is shown below

<img width="800" alt="lab1-gtkwave" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/gtkwave_good_mux.png">

## Introduction to Yosys
It is the synthesizer used to convert RTL to netlist.
Netlist should be the same as the Design but represented in the form of standard cells.
The same testbench can be used to verify RTL and Synthesized Netlist.

<img width="800" alt="intro_yosys" src="https://github.com/sukanyasmeher/sfal-vsd/assets/166566124/0920be6f-770d-447d-a2cf-eaf73280539e">

## Introduction to Logic Synthesis

<img width="800" alt="intro_logic_synthesis1" src="https://github.com/sukanyasmeher/sfal-vsd/assets/166566124/d01c7771-7bb7-42cd-b7a1-24472ca61226">

## Lab using Yosys and Sky130 PDKs

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 001.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 002.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 003.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 004.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 005.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 006.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 007.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 008.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 009.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 010.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 011.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 012.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 013.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 014.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 015.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 016.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 017.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 018.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 019.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 020.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 021.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Read_Liberty 022.png">

<img width="800" alt="yosyslab1" src="https://github.com/lhademmor/SFAL-VSD-SoC/blob/main/pictures%20of%20progress/Yosys Show.png">

</details>
