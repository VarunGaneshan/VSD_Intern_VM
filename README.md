# **VSD_Research_Internship_Project_VLSI**
## Vending_Machine_with_Change_System
I will be implementing an **Ideal** Vending Machine with Change System. The project aims to match the functional simulation results obtained from the RTL netlist and Gate-Synthesized netlist as closely as possible.

**Technology used: Sky130 technology**

>Through this Repo, I intend to document my weekly learnings & progress for this project and also contribute to the opensource community.

>Reach out to me @ [LinkedIn](https://www.linkedin.com/in/varung-1x/)

<details>
 <summary> RTL2GDS flow & tools required(VSD openEDA course) </summary> 
	
>Complete flow toolchain - **Qflow**

>Static Timing Analysis mandatory at every stage,tool - **Opentimer**
- RTL netlist
>Logic Synthesis tool - **Yosys open synthesis suite**
- Through Logic synthesis you get Logical netlist(gates&flipflops)
>IC design flow tool(FP,placement,CTS) - **Graywolf**
- Floorplanning
- Placement of logical cells
>Layout viewer at any stage to correct DRC,tool - **MAGIC**
- Clock Tree Synthesis(to get the specified skew)
>Routing toll - **Qrouter**
- Routing
- Signoff - gds out to fabrication
>Pre/Post layout Simulation,tool - **ngSPICE**

>Schematic editor,tool - **eSim**

</details>	

###  Week1_Task1 (Tool Installation)

<details>
 <summary> Work </summary>
To install all the necessary tools required for this project.Refer to the course(VSD openEDA) to install Virtual box with Ubuntu 20.04+,allocate 6-8GB RAM,4CPU and 40GB Disk Space.Install the following tools:
	
- iverilog

- gtkwave

- yosys
</details>	

<details>
 <summary> iverilog </summary>
 
```bash
sudo apt-get install iverilog
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/95de84c2-8752-4888-8a0c-f38f6ef44585)

After launch 

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/0238a323-29d9-469f-877a-f63a053e7020)

</details>	

<details>
 <summary> gtkwave </summary>

```bash
(paste each line seperately)
sudo apt update
sudo apt install gtkwave
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/2958abbd-740b-4721-aac3-2af69e0fcff9)

After launch

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/638882c0-5119-481d-860d-679a62039621)

</details>	

<details>
 <summary> yosys </summary>
	
 ```bash
(paste each line seperately)
sudo apt-get install git
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make
sudo apt-get install build-essential clang bison flex \libreadline-dev gawk tcl-dev libffi-dev git \
graphviz xdot pkg-config python3 libboost-system-dev \ libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/6f41ef80-39c0-4206-8017-04f8629178dd)
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/4a9a5ea5-17f9-4841-8244-ac77fe5d1d47)

After launch

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/9f4b4e66-3c42-43ef-9c7b-61bb31642816)

</details>	

###  Week1_Task2 (Design Specs)

<details>
 <summary> Work </summary>
Understand the Working and Identify the following for the Vending Machine:
 
- Input ports

- Output ports

- Input waveforms

- Output waveforms

</details>	

<details>
 <summary> Specifications </summary> 
<p><b>Block Diagram:</b></p>
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/197aa813-3166-49ce-9ffc-fd0bef84b701)

| S.No   | Name of the Port  | Direction  | Size | Description |
|------------|------------|------------|--------|-----|
| 1. | Product     | Output     |1| Successful Transaction or Not|
| 2.     | Change    | Output     | 2 | Excess Amount that is to be Returned |
|      |     |      |  | Rs.5(01) and Rs.10(10)|
| 3.     | Coins     | Input     | 2 | Amount Inserted |
|      |     |      |  |Rs.0(00) , Rs.5(01) and Rs.10(10)|
| 4.     | Clk   | Input      | 1 |  Clock Signal-Synchronize|
| 5.     | Rst    | Input     | 1 | Reset Signal|
| 6.     | Current_State    | Intermediate     | 2 | Store the Current State|
| 7.     | Next_State    | Intermediate     | 2 | Store the Next State|

<p><b>Assumptions:</b></p>

- Only one type product is present in the machine.
- Each Product costs Rs.15.
- Only Currency denominations are Rs.5 and Rs.10.

<p><b>State Diagram:</b></p>

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/ce7754d3-e378-4a7d-8e55-8406f6ad9e39)

- Each state signifies the current amount which is inside the machine.
- Next state is copied to current state for every cycle.
- Ideal Vending machine here means,as shown in S1 to S0 (0/0,c=5) transaction,the machine should return the change when the user does not add the cost amount after waiting for a certain time(here the end of simulation).

</details>	

<details>
 <summary> Waveforms </summary>

>rst off at #6,changes starts to reflect from #10(1st posedge of clk after rst=0).

<p><b>Coin insertion-5,5,5:</b></p>
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/ae156ab6-a678-4299-9d2a-db0cde92c84c)

>Product returned at #35.

<p><b>Coin insertion-5,10:</b></p>
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/df62856e-9dfe-47c9-92f1-eef945cb9fd9)

>Product returned at #25.

<p><b>Coin insertion-10,10:</b></p>
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/b35dc89b-430d-41f3-9ce9-ee8f8f7983a5)

>Product returned at #25 with change of 5 rs.

<p><b>Coin insertion-10,0:</b></p>
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/cb7ba44c-3452-4e15-8dd3-c392121d503f)


>Change of 5 rs returned at #25

</details>	

###  Week2_Task1 (Basics of Functional Simulation)

<details>
 <summary> Work </summary>
Familiarize using the tools for functional simulation:

- Clone the github repo sky130RTLDesignAndSynthesisWorkshop which has standard verilog source files and its testbench.
  
- Load a design into the iverilog simulator

- Execute the a.out file

-  Run the vcd file created in gtkwave simulator


</details>	

<details>
 <summary> Theory </summary>
	
<p><b>Introduction:</b></p>

- RTL Design: RTL Design refers to the actual Verilog code or a set of Verilog codes that encapsulates the intended functionality to fulfill specified requirements. Register Transfer Level (RTL) serves as an abstraction for defining the digital aspects of a design, representing a fundamental framework in contemporary electronic system definitions. Often regarded as the cornerstone in the design and verification process, RTL design is typically expressed using hardware description languages (HDL) like Verilog or VHDL.

- Test Bench: A test bench constitutes the environment set up to provide stimuli (test vectors) to the design under evaluation to assess its functionality. By subjecting the design to stimuli and observing its outputs, one ensures compliance with the specified requirements. This process involves verifying whether the design's behavior aligns with the given specifications.
	
- Simulation: Simulation involves executing the design model written in HDL, following successful compilation and elaboration, based on a specified execution model. Utilizing simulation software (simulator), it verifies the functional correctness of a digital design described in a hardware description language (HDL) such as VHDL or Verilog. It ensures adherence to given specifications.

- Simulator: A tool used for simulating the design, such as "iverilog" in this context. RTL design embodies the required specifications' implementation, and its functionality is verified by simulating the design using a simulator.

- How does a simulator work? A simulator operates by continuously monitoring input changes. Upon any alteration in inputs, the output undergoes re-evaluation. If there is no input change, output evaluation is bypassed. The simulator records input changes and corresponding output states into a file.
  
<p><b>Design and Test Bench setup:</b></p>

- The Verilog code representing the RTL design typically features primary inputs and primary outputs, which may vary in number. These primary inputs and outputs serve as the interfaces between the design and its external environment.

- To validate the functionality of the design, stimuli must be applied to all primary inputs, and the resulting behavior at the primary outputs must be observed. This necessitates the use of a stimulus generator at the input and a stimulus observer at the output.

- In the test bench, the design module is instantiated, allowing stimuli to be applied. It's essential to understand that while the test bench orchestrates the testing process by instantiating the design module and applying stimuli, it itself does not possess any primary inputs or outputs. Instead, it serves as the framework within which the design is tested, facilitating the verification process without directly interacting with the design's primary interfaces.

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/d6b61c59-91ef-499c-bb8d-75bde0340e65)

<p><b>Simulation Flow:</b></p>

- Inputs to the simulator:
The iverilog simulator processes two primary inputs:

   * RTL Design: This represents the behavioral description of the specifications in a hardware description language (HDL), such as Verilog.
   * Test Bench: The test bench serves as the environment to apply stimuli or test vectors to the design, ensuring functionality and correctness. It instantiates the Verilog module of the design and provides stimuli to the input ports of the RTL design.

- Output of the simulator:
The iverilog simulator generates a value change dump (.vcd) file as its output. This file captures the changes in signal values during simulation. The vcd file can be visualized using the GTKWave viewer tool, facilitating the analysis of simulation results.

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/f25d9598-60c4-425f-b694-8e22d2a495e7)

</details>	

<details>
 <summary> Commands </summary>
<p><b>Setup:</b></p>

```bash
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/
```
>lib: Contains sky130 standard cell library(sky130_fd_sc_hd__tt_025C_1v80.lib)

>verilog_model: Contains verilog model of standard cells in lib directory(primitives.v,sky130_fd_sc_hd.v)

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/a2ccbd89-a975-4c4e-96d0-78a03d4d9a63)

```bash
cd verilog_files/
ls
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/ba601226-f129-4379-9a38-b3c41c50fcd7)

<p><b>Simulation of Multiplexer:</b></p>

```bash
iverilog good_mux.v tb_good_mux.v
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/42053a23-f2b9-4a5e-a545-cb4f6b05a9b8)

```bash
ls
./a.out
gtkwave tb_good_mux.vcd
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/a6b20985-6253-4380-b6f3-dff7aa5b3b68)

</details>	

<details>
 <summary> Output Waveforms </summary>
	
<p><b>Mux Truth table:</b></p>

| Select Signal(sel) | Inputs(i1 i0) | Outputs(y) |
|------------|------------|------------|
| 0     | 0 0    | 0    |
| 0     | 0 1   | 1     | 
| 1     | 1 0      | 1     | 
| 1     | 1 1   | 1      |

>When sel=0,y=i0 

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/c06300ae-33f8-4424-a199-aacbde8b3303)

>When sel=1,y=i1

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/8f560e1f-328f-4aa8-b2c7-1a8d4e664658)

</details>	


###  Week2_Task2 (Basics of Synthesis,Gate Level Simulation)

<details>
 <summary> Work </summary>
Familiarize with the commands for Synthesis.Yosys is the Synthesizer used here to convert RTL(good_mux) to its gate netlist(F2).
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/10c2327e-bdd1-4ced-97c5-6e8fd9f2566e)

</details>	

<details>
 <summary> Theory </summary>
<p><b>Yosys setup:</b></p>
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/3a8ef4cc-a83c-4364-84da-97b6aa9857ca)

- .lib file is an ASCII representation of timing and power parameter associated with cells inside the standard cell library of a particular technology node.

- netlist file is the representation of the design in form of the standard cells in .lib.

<p><b>Verify the Synthesis:</b></p>

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/06322798-9582-423b-b3f6-e9dde7541b6e)

- The stimulus generated must match the output from the rtl simulation.

- Primary Input/Output remains the same in both RTL code & Netlist,So the same testbench can be used for verification.
</details>	

<details>
 <summary> Commands for synthesis </summary>

```bash
yosys
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/ded33780-1437-46d6-a160-78b8d26ca1c2)

```bash
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib #read .lib,relative path wrt verilog_files
read_verilog good_mux.v #read design
synth -top good_mux #synthesize the module
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/d869b022-4f20-4630-8a5b-8758cd0f67e4)

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/3eec8b0c-1b6b-496b-9902-5c223317308c)

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/9df95984-17f9-4125-af2a-3b919d9c68e5)
```bash
gvim good_mux.v
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/90a5dbfc-a5c7-456c-82b0-9bba1ee7f833)

```bash
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  #generate netlist
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/f488996a-2674-4d68-a924-4c65f6ce9a44)

```bash
show 
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/31703d43-e3c3-4e2e-ad75-69353a3e1250)

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/7ae50537-27cb-4dcc-a920-81ad4fc7f642)
```bash
write_verilog good_mux_netlist.v #write netlist
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/89045b7c-5c0c-4953-894d-c4f74879b343)
```bash
vim good_mux_netlist.v 
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/74436368-b327-444a-9e8c-6c3290535876)
```bash
write_verilog -noattr good_mux_netlist.v
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/cb1535c3-680b-40e3-b22a-d8f804b29445)
```bash
!gvim good_mux_netlist.v
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/2c046c13-b81e-4deb-bf27-7ce193c304ec)

</details>	

<details>
 <summary> Waveforms from GLS </summary>
<p><b>Pre-Synthesis Simulation:</b></p>
	
```bash
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/d2d0cf03-e998-4a61-a9bd-fde71074b171)

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/ddff77d8-bfec-4168-ad82-6530e9c1b87d)


<p><b>Post-Synthesis Simulation:</b></p>
	
```bash
iverilog good_mux_netlist.v tb_good_mux.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ../my_lib/verilog_model/primitives.v
./a.out
gtkwave tb_good_mux.vcd
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/74e933e4-798a-4753-8c78-141014b79a91)

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/fa28a05e-8a05-4159-8b16-2cb5a9c07760)

<p><b>We can observe that the results from both functional simulation and gate level simulation match.</b></p>

</details>	

###  Week3_Task1 (VM-Functional Simulation)

<details>
 <summary> Work </summary>
Functional simulation of my vending machine's verilog netlist and testbench in iverilog and gtk wave.
  
- Load the design into the iverilog simulator

- Execute the a.out file

-  Run the vcd file created in gtkwave simulator

</details>	

<details>
 <summary> Commands </summary>
			    
```bash
mkdir VM
cd VM
mkdir verilog_codes
cd verilog_codes/
gvim vending_machine.v
gvim vending_machine_tb.v
ls
iverilog vending_machine.v vending_machine_tb.v
ls
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/3507aa35-1e29-4ac1-8748-edba7782d2fa)

```bash
./a.out
gtkwave vending_machine_tb.vcd
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/e70e2faf-368e-443b-941b-b1357be29af0)

</details>	

<details>
 <summary> Output Waveforms </summary>

>To change the inputs,change the time specifications for input signal in tb.

<p><b>Coin insertion-5,5,5:</b></p>

```verilog
#6 rst = 0;
in = 1;
#11 in = 1;
#16 in = 1;
#25 $finish;
```
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/42530122-6d4e-47cd-8e6d-0082a48e9003)

<p><b>Coin insertion-5,10:</b></p>

```verilog
#6 rst = 0;
in = 1;
#11 in = 2;
#25 $finish;
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/4ccc4b39-403d-42cc-87da-1c3f1ef69eff)

<p><b>Coin insertion-10,10:</b></p>

```verilog
#6 rst = 0;
in = 2;
#11 in = 2;
#25 $finish;
```

![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/125fb727-0797-4260-b8af-5878fe77005a)

<p><b>Coin insertion-10,0:</b></p>

```verilog
#6 rst = 0;
in = 2;
#11 in = 0;
#25 $finish;
```
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/48b5261e-3c51-48d6-8e19-9654e4f5073b)

</details>




##  References 

> Refer to this course for all the open source tools installation - [VSD openEDA](https://www.udemy.com/course/vsd-a-complete-guide-to-install-open-source-eda-tools/learn/lecture/6719216#overview)

>[Link](https://www.youtube.com/watch?v=tJc0blBDRzo)- helped me to understand the working of an ideal vending machine. Also refer to his playlist for more rtl projects in verilog.

>[Link](https://teamvlsi.com/2020/05/lib-and-lef-file-in-asic-design.html)- about .lib file in vlsi.

>[Link1](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax),[Link2](https://www.youtube.com/watch?v=Nj87GEXxhjc),[Link3](https://gist.github.com/citrusui/07978f14b11adada364ff901e27c7f61)- helped me to understand basic github documentation.Refer to the code of someone's README file to understand the syntax for a particular format that you want to replicate.

