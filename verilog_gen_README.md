## Understanding the Verilog Generation flow


The verilog files to be used for the RTL to GDS flow are generated in this step.

<b> Inputs </b> : Verilog template files <br>

![image](https://user-images.githubusercontent.com/110677094/200527567-3d2dad7e-c29a-4670-ba89-8090c08eea5b.png)


<b> Outputs </b>: Verilog netlist files which contain the description of the circuit.

The input parameters are taken from the modelfile.csv and the specifications are taken from test.json file.

### Block Diagram
![image](https://user-images.githubusercontent.com/110677094/199850293-d556bbeb-89ec-4315-ba20-0db28d745d5a.png)


### Detailed explanation

The generated aux_cells based on above mentioned parameters are used to generate the netlist files.

This step can either be done using below command, which performs the verilog generation
```
make sky130hd_temp_verilog
```
OR 

it is also the first step when running the entire flow using the below command
```
make sky130hd_temp
```

When the above commands are run, the ``` openfasoc/generators/temp-sense-gen/tools/temp-sense-gen.py ``` is executed and it performs the following.

It uses the digital standard cells and aux cells to generate netlist verilog files. The netlist verilog files are generated using the function temp_gen_netlist from the TEMP_netlist class. 

![image](https://user-images.githubusercontent.com/110677094/199847445-ed6dd528-9a8c-4758-bab2-3abf0b9b4bc3.png)


Here the the placeholders in the verilog template files are replaced with the aux_cell info.
The difference between the template and the generated verilog file can be found below. (one of the example)

![image](https://user-images.githubusercontent.com/110677094/199847173-cab169f4-2063-4db7-b3c2-c2c5d39c432f.png)


The temp_gen_netlist function can be found in ``` openfasoc/generators/temp-sense-gen/tools/TEMP_netlist.py ````

![image](https://user-images.githubusercontent.com/110677094/199847634-622e770d-12ff-4249-800d-598fb053c417.png)


Once the netlist files are created, the header cells, the lv cells info is stored in files named 'blocks/sky130hd/tempsenseInst_custom_net.txt' and 'blocks/sky130hd/tempsenseInst_domain_insts.txt' in the src directory.

The new netlist files are now available in the ```OpenFASOC/openfasoc/generators/temp-sense-gen/src folder``` and the ```OpenFASOC/openfasoc/generators/temp-sense-gen/flow/design/src/tempsense ```

![image](https://user-images.githubusercontent.com/110677094/199846734-bf7d562c-5bc4-4dfa-993c-4c7c5a601867.png)

The generated netlist files are as follows:

- counter.v from counter_generic.v
- TEMP_ANALOG_hv.nl.v from TEMP_ANALOG_hv.v
- TEMP_ANALOG_lv.nl.v from TEMP_ANALOG_lv.v


Check below image for the terminal output
![image](https://user-images.githubusercontent.com/110677094/198141448-52d93700-bd0a-4ce1-985a-d3c1c1955efd.png)


## Refer to the below git repositories for the steps done after verilog generation:

Floorplan:                      https://github.com/ParasVekariya/OpenFASOC_Floorplan                                         <br>
Floorplan and CTS:              https://github.com/m4ury4p/OpenFAASoc_flow                                                   <br>



<br></br><br></br><br></br><br></br>
