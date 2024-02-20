# **VSD_Internship_Project**
## Vending_Machine_with_Change_System
My design is a **Vending Machine with Change System**. The project aims to match the functional simulation results obtained from the RTL netlist and Gate-Synthesized netlist(logic synthesis) as closely as possible.

>Through this Repo, I intend to document my weekly learnings & progress for this project.

>[Link1](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax),[Link2](https://www.youtube.com/watch?v=Nj87GEXxhjc),[Link3](https://gist.github.com/citrusui/07978f14b11adada364ff901e27c7f61)- helped me to understand basic gihub documentation.

##  Week1_Task1

### Notes:
RTL2GDS flow:
>Static Timing Analysis mandotary at every stage,tool - **Opentimer**
- RTL netlist
>Logic Synthesis tool - **Yosys open synthesis suite**
- Through Logic synthesis you get Logical netlist(gates&flipflops)
>IC design flow tool - **Graywolf**
- Floorplanning
- Placement of logical cells
>Layout viewer at any stage to correct DRC,tool - **MAGIC**
- Clock Tree Synthesis(to get the specified skew)
>Routing toll - **Qrouter**
- Routing
- Signoff - gds out to fabrication
>Pre/Post layout Simulation,tool - **ngSPICE**
>Schematic editor,tool - **esim**
### Work
To install all the necessary tools required for the project. I have already installed VirtualBox with Ubuntu 22.04.
- iverilog
- gtkwave
- yosys

### iverilog

### gtkwave

### yosys
