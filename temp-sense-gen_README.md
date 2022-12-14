# openFasoc_Flow
<h4> Verification of existing openFasoc flow </h4>

FASoC stands for Fully Autonomous System-on-Chip

The FASoC Program is focused on developing a complete system-on-chip (SoC) synthesis tool from user specification to GDSII. FASoC leverages a differentiating technology to automatically synthesize “correct-by-construction” Verilog descriptions for both analog and digital circuits and enable a portable, single pass implementation flow. The SoC synthesis tool realizes analog circuits, including PLLs, power management, ADCs, and sensor interfaces by recasting them as structures composed largely of digital components while maintaining analog performance. They are then expressed as synthesizable Verilog blocks composed of digital standard cells augmented with a few auxiliary cells generated with an automatic cell generation tool. By expanding the IPXACT format and the Socrates tool from ARM, we then enable composition of vast numbers of digital and analog components into a single correct-by-construction design. This project is led by a team of researchers at the Universities of Michigan, Virginia, and Arm.

<h4> Tool installation steps can be found here: </h4>

https://openfasoc.readthedocs.io/en/latest/getting-started.html#installation

You can either follow the express installation or the manual installation steps.

The following tools will be required
1. OpenRoad
2. Magic
3. Yosys
4. Klayout
5. Open_PDK
6. Netgen

Note: Miniconda installation might help in easy installation

Make sure to download and install all the required dependencies as mentiioned in the link above.

If you are facing issues in installating Klayout, follow below steps:
1. Go to the below mentioned website and install the suitable klayout version package for your OS
https://www.klayout.de/build.html
2. Follow one of the below for installation
```
sudo dpkg -i <packagename>.deb
cd klayout-*
./build.sh
````
If ./build.sh doesn't work, try ``` sudo ./build.sh ``` or ``` sudo bash ./build.sh ```

OR 

```
sudo apt-get install <packagename>.deb
```

## Refer to the below git repositories for the steps done before verilog generation:

Aux cell generation:                      https://github.com/drvasanthi/OpenFASOC.git                                         <br>
Description of GDS and LEF of aux cells:  https://github.com/DebanganaMukherjee/OpenFASOC                                     <br>
Description of CDL and LIB of aux cells:  https://github.com/Bandaanusha/OPENFASOC/blob/main/Aux_cell_generator_outputs.md    <br>
For generation of verilog templates:      https://github.com/agarwal-kavya/OpenFASOC                                          <br>
                                          https://github.com/suysh-msra/OpenFASOC                                             <br>



### OpenFASoC flow 

![image](https://user-images.githubusercontent.com/110677094/199426029-2676771d-e8bc-406f-bf9c-22f617aab4aa.png)


<h4> Running the OpenFASOC Flow for temperature sensor generator </h4>

1. Clone the openfasoc git repo using the below command

```
git clone https://github.com/idea-fasoc/openfasoc
```

2. Move to the required temp-sense-gen directory 
```
cd openfasoc/generators/temp-sense-gen
```

3. Give the following commands

```
make

```

![image](https://user-images.githubusercontent.com/110677094/198135692-616313f9-68f3-493f-816b-73f091eef640.png)

```
make sky130hd_temp
```
This will create the macro for the thermal sensor, creates the lef/def/gds files and performs lvs/drc checks. It won't run simulations.

![image](https://user-images.githubusercontent.com/110677094/198135936-98aaec16-ad55-48e7-8def-fc932b769157.png)

<h4> Running Synthesis and APR </h4>

![image](https://user-images.githubusercontent.com/110677094/198136347-0871fcbe-b11c-4ef4-ad29-9933c8e5831e.png)

<h4> Floorplan Results </h4>

![image](https://user-images.githubusercontent.com/110677094/198136608-2bb01a10-ab23-477f-aee5-5ca1c2308872.png)

Observe below floorplan timing, power and area stats

![image](https://user-images.githubusercontent.com/110677094/198136780-8d9e0694-09b9-4966-b8dc-c76297af7375.png)

Global placement timing reports

![image](https://user-images.githubusercontent.com/110677094/198137210-75a2d74b-b561-4888-8e3d-3a53bfaca9e9.png)

![image](https://user-images.githubusercontent.com/110677094/198137389-0ac4c572-defe-4933-8ccd-1027eeb78443.png)

Global placement power and area stats

![image](https://user-images.githubusercontent.com/110677094/198137460-4329a005-32a2-4dd9-b431-2064868d4d80.png)

![image](https://user-images.githubusercontent.com/110677094/198137719-069de85d-d636-4d3e-b1ac-0fce8568877c.png)

Detailed placement reports

Timing report

![image](https://user-images.githubusercontent.com/110677094/198137963-76a03034-14a7-4c90-8371-61538989824b.png)

Slew, capacitance and fanout checks

![image](https://user-images.githubusercontent.com/110677094/198138295-fb46e910-0e80-4754-b7f1-41a9e6b15c45.png)

Detailed placement power report

![image](https://user-images.githubusercontent.com/110677094/198138473-50fc5271-967a-409f-bb23-b2396cb6e82c.png)

Routing resources analysis

![image](https://user-images.githubusercontent.com/110677094/198138650-8a8fd0d7-89a7-482e-8b37-d5772ed1171a.png)

Global routing timing report (report_checks)

![image](https://user-images.githubusercontent.com/110677094/198138758-eff674d2-57a0-4e77-ae76-3835f23ca636.png)

Global routing power and area stats

![image](https://user-images.githubusercontent.com/110677094/198138827-019f9897-0297-47cd-ac50-5744d9db7b30.png)

![image](https://user-images.githubusercontent.com/110677094/198138904-a6393502-4b6e-43b8-9d74-735b3776f738.png)

![image](https://user-images.githubusercontent.com/110677094/198139204-3679f670-e444-49c6-b74f-be7121a44765.png)

![image](https://user-images.githubusercontent.com/110677094/198139299-988823ae-6d50-4303-981b-6c9b689823cb.png)

![image](https://user-images.githubusercontent.com/110677094/198139365-a3a850c4-d390-4ade-b07a-7ea9d91283c9.png)

![image](https://user-images.githubusercontent.com/110677094/198139741-866dfa0c-599b-4386-bf7f-529bc643e14d.png)

![image](https://user-images.githubusercontent.com/110677094/198139850-a05eb2f5-0dd5-4f32-9d05-16c73b13409c.png)

Finish Power report

![image](https://user-images.githubusercontent.com/110677094/198140225-4fafc61b-313a-4ffe-bfd8-de3ebb4a43cc.png)

Finish area report

![image](https://user-images.githubusercontent.com/110677094/198140344-8972c13e-4114-4d34-b359-a59cb7e7a7ca.png)

Place and Route is finished

![image](https://user-images.githubusercontent.com/110677094/198140436-9973441f-06a4-464f-84e5-32a8b5b9584a.png)

DRC is finished

![image](https://user-images.githubusercontent.com/110677094/198140519-1e0fbde2-8a4b-4799-88ca-ce5b0e9c6e80.png)


![image](https://user-images.githubusercontent.com/110677094/198140579-36c67d19-4944-4397-a38c-6dbfaba3fdcb.png)

![image](https://user-images.githubusercontent.com/110677094/198140711-b29a5240-78b3-4376-851b-34da3760160a.png)

![image](https://user-images.githubusercontent.com/110677094/198140807-0aa0c0b3-c1cb-4dd1-8c72-1fba516d329e.png)

![image](https://user-images.githubusercontent.com/110677094/198140904-bf995532-21c1-40a7-9d40-f12f9d80ab0a.png)

![image](https://user-images.githubusercontent.com/110677094/198140966-83111655-06e8-4bb0-a39e-6a2dad8b02b6.png)

![image](https://user-images.githubusercontent.com/110677094/198141034-a198141f-37b5-412b-bd29-7a9e7c046f33.png)

![image](https://user-images.githubusercontent.com/110677094/198141181-66fc0f90-2ef4-4656-8a04-888df6beae8d.png)

![image](https://user-images.githubusercontent.com/110677094/198141297-2dfc1f55-0871-49d1-b1b8-3153e27f8231.png)

LVS is now finished

We can see the messages that DRC and LVS is clean and macro is generated. 
The final result displays <b>Circuits match uniquely</b>

The results are available in ``` tempsensegen/work ``` directory
It contains files as below
6_final_drc.rpt
6_final_lvs.rpt
tempsenseInst_error.gds


Final GDS Layout viewed using Klayout

![image](https://user-images.githubusercontent.com/110677094/199008858-b1249029-76c4-4838-aa96-085209cba271.png)


We can also try below commands and observe the flow

```
make sky130hd_temp_verilog
```


![image](https://user-images.githubusercontent.com/110677094/198141448-52d93700-bd0a-4ce1-985a-d3c1c1955efd.png)

```
make sky130hd_temp_full
```

![image](https://user-images.githubusercontent.com/110677094/198141606-01ef7e86-eee1-49b0-b01e-17974299ad89.png)

![image](https://user-images.githubusercontent.com/110677094/198141917-03257451-c49f-4522-ba6d-e83b8ba2b21f.png)

![image](https://user-images.githubusercontent.com/110677094/198245866-5eb9ac6a-d088-4e96-8a1b-7f93997dd1e9.png)
