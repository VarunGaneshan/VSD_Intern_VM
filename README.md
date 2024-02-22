# **VSD_Research_Internship_Project_VLSI**
## Vending_Machine_with_Change_System
I will be implementing an **Ideal** Vending Machine with Change System. The project aims to match the functional simulation results obtained from the RTL netlist and Gate-Synthesized netlist as closely as possible.

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

###  Week1_Task2 (Identifying I/O)

<details>
 <summary> Work </summary>
Identify the following for the Vending Machine:
 
- Input ports
- Output ports
- Input waveforms
- Output waveforms
</details>	

<details>
 <summary> Design </summary>
Block Diagram
	
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/197aa813-3166-49ce-9ffc-fd0bef84b701)

State Diagram
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/ce7754d3-e378-4a7d-8e55-8406f6ad9e39)
</details>	

<details>
 <summary> Waveforms </summary>

	
5,5,5
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/233c01ae-9b40-483e-acd8-2f80980ca053)
5,10
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/45168ca9-2f48-4711-af89-4b11162f8cdb)
10,10
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/0d012f06-909e-4e03-abfb-dab5a1902c43)
10,0
![image](https://github.com/VarunGaneshan/VSD_Intern_VM/assets/94780009/c6766e91-45fd-48f4-b282-aa9aacf74b4c)
</details>	

##  References 

> Refer to this course for all the open source tools installation - [VSD openEDA](https://www.udemy.com/course/vsd-a-complete-guide-to-install-open-source-eda-tools/learn/lecture/6719216#overview)

>[Link](https://www.youtube.com/watch?v=tJc0blBDRzo)- helped me to understand the working of an ideal vending machine. Also refer to his playlist for more rtl projects in verilog.

>[Link1](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax),[Link2](https://www.youtube.com/watch?v=Nj87GEXxhjc),[Link3](https://gist.github.com/citrusui/07978f14b11adada364ff901e27c7f61)- helped me to understand basic github documentation.Refer to the code of someone's README file to understand the syntax for a particular format that you want to replicate.

