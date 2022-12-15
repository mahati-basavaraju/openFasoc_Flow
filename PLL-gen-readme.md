# PLL Generation using OpenFaSoC

## PLL

A phase-locked loop (PLL) is an electronic circuit with a voltage or voltage-driven oscillator that constantly adjusts to match the frequency of an input signal. PLLs are used to generate, stabilize, modulate, demodulate, filter or recover a signal from a "noisy" communications channel where data has been interrupted.

PLLs are widely used in wireless or radio frequency (RF) applications, including Wi-Fi routers, broadcast radios, walkie-talkie radios, televisions and mobile phones.

At its simplest, a phase-locked loop is a closed-loop feedback control circuit that's both frequency- and phase-sensitive. A PLL is not a single component, but a system that consists of both analog and digital components -- interconnected in a "negative feedback" configuration. Consider it analogous to an elaborate operational amp (op amp)-based amplifier circuit.

In the PLL to be designed,

- the analog blocks are 

1. Charge Pump (CP)
2. Voltage Controlled Oscillator (VCO)

- the digital blocks are 

1. Frequency Detector (FD)
2. Phase Frequency Detector (PFD)

This design of PLL is referenced from https://github.com/lakshmi-sathi/avsdpll_1v8'

## Building blocks in the OpenFaSoC flow

### Analog Block Generation

The gds and lef for analog blocks can be generated intelligently using an open-source tool named ALIGN.

For more information on ALIGN, refer to the git repository given below.
- https://github.com/ALIGN-analoglayout/ALIGN-public

A spice netlist has been individually written for both CP and VCO from which the gds and lef for both of them will be generated. These two blocks are knwon as auxiliary cells.
For further information on the netlists, simulation results and final outputs from ALIGN tool, refer to below repositories.
- https://github.com/sanampudig/OpenFASoC
- https://github.com/drvasanthi/OpenFASOC/tree/main/PLL_GEN
- https://github.com/Bandaanusha/OPENFASOC

The gds and lef of above blocks are present in ``` PLL-gen/blocks/gds ``` and ``` PLL-gen/blocks/lef ```


### Digital Block Generation

Verilog files have been written for both PD and PFD.

### Verilog File Generation

A PLL.v file is written which instantiates or uses each of the above mentioned digital and analog blocks which comprises of the entire PLL design.

### Model file 

The model file contains the parameters i.e, the minimum (3 MHz) and maximum(12.5 MHz) frequency for the PLL to match.

### Platform configuration

Sky130 PDK is the platform on which the flow will be run. So the path to the libs.tech and libs.ref of sky130A is given the platform_config.json file.

### Run the OpenFaSoC flow

- Open terminal in the below directory path
```/home/<username>/OPENFASOC/openfasoc/generators/PLL-gen/```

- Run the make command below to run the flow
```make sky130hd_pll```

![image](https://user-images.githubusercontent.com/110677094/207930755-c1a7fb6c-7724-43a8-8d60-985dc8ccc14e.png)


- Synthesis, Placement and Routing 
  - Synthesis Finished
    ![image](https://user-images.githubusercontent.com/110677094/207931031-5da13783-15b1-4b39-b213-a5e08819a433.png)

  - Floorplan
    ![image](https://user-images.githubusercontent.com/110677094/207931279-65dbbdf3-2dbc-45b2-a81a-a2c84d58e231.png)

    Floorplan Reports
    ![image](https://user-images.githubusercontent.com/110677094/207931483-686c8e20-eed2-4217-a7d6-7d1501c2f540.png)

    ![image](https://user-images.githubusercontent.com/110677094/207931630-b7601419-69ce-4753-9e3f-ebf6ebc5630d.png)

  - Placement
    ![image](https://user-images.githubusercontent.com/110677094/207931736-30b73174-b459-4a9b-ad31-dcb02164b5d8.png)

    Global Placement Report
    ![image](https://user-images.githubusercontent.com/110677094/207932084-6385fb2f-4864-45db-b84f-cb99255ad22c.png)

    Placement Analysis
    <br/>
    ![image](https://user-images.githubusercontent.com/110677094/207932710-a36c3d6e-52d4-425d-ad5f-27e23de45570.png)

    Detailed Placement Report Checks
    ![image](https://user-images.githubusercontent.com/110677094/207932920-36329023-7408-49d0-af5f-110c4bd0cda9.png)
    
    Detailed Placement Power Report
    ![image](https://user-images.githubusercontent.com/110677094/207933010-09126050-7a8b-47cf-9e9d-66390c614fe7.png)
 
 - Routing
   ![image](https://user-images.githubusercontent.com/110677094/207933581-0229b8c6-61a1-4d46-81dc-cc3b4db31fec.png)

  Note that in this phase, an error is encountered as shown in the image below
  ![image](https://user-images.githubusercontent.com/110677094/207933811-23ca5f57-45fd-4750-88b3-658cc01e8af0.png)

  Resolving this error, is a part of future work.
  
### Details
For detailed analysis on PLL-generation, verilog files generation, changes to be done, errors encountered and future, please refer to the below repository
<br/>
https://github.com/vinayrayapati/OpenFaSoc
    

## References

1. https://www.techtarget.com/searchnetworking/definition/phase-locked-loop
2. https://github.com/lakshmi-sathi/avsdpll_1v8
3. https://github.com/vinayrayapati/OpenFaSoc
4. https://github.com/sanampudig/OpenFASoC
5. https://github.com/drvasanthi/OpenFASOC/tree/main/PLL_GEN
6. https://github.com/Bandaanusha/OPENFASOC

## Acknowledgment
- Kunal Ghosh, Director, VSD Corp. Pvt. Ltd. kunalghosh@gmail.com
- Vinay Rayapati
- Gopala Krishna Reddy Sanampudi
- Ravi Kiran Reddy Gogireddy
- Gandi Ajay Kumar 
- Vasanthi D R
- Anusha Banda

## Author

Mahati Basavaraju, MS by Research Student @ IIIT Bangalore
