# SOC_Design_and_planning_NASSCOM_VSD
### Implementation

#### The synthesis of a design picorv32a is processed in this step, a design with a default time period of 20ns and some sdc constraints, a verilog RTL, a clock port as shown as below:

## DAY 1 :- 
1) Visiting all the directories for basic understanding of the files
2) Synthesis Flow of the design "picorv32a"
3) Calculate the flop ratio

INFO :
1) LEF'S are merged during synthesis flow (TECH LEF and STD LEF)
2) We can make our own version of CONFIG.tcl for unique clock constraints
3) Runs directory is created with tmp, results, reports folders
4) Logs file mention all the steps occured in the flow

```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100 
```
so flop ratio is 1613/14876 * 100 = 10.84 %

* All section 1 logs, reports and results can be found in following run folder:

[Section 1 Run](https://drive.google.com/file/d/1Be5T9Z0SsT0eHPfNZKv3csnGbdd7dQjv/view?usp=sharing)

#### 1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform synthesis

```bash
# Change directory to openlane flow directory to move to the synthesis working software
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'

```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode 
./flow.tcl -interactive

# Now that OpenLANE flow is running we have to run it with proper version and packages
package require openlane 0.9

# We are here to run the design 'picorv32a' so we are preparing it for the flow..
prep -design picorv32a

# we can run synthesis using following command to complete the synthesis
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker to complete the flow and return back to the terminal
exit
```

Results 

![1](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-07-30%20162523.png)


#### Summary
1) The final result shows "synthesis is done" in the terminal.
2) Openlane allows to make changes on the run
3) GITHUB repo of openlane is viewed and understood

## DAY 2:-
1)Understanding floorplan pin placement
2)Recognising floorplan parameters and standard cell placement
3)Understanding clock, power parameters and the conditions
4)Understanding switches and parameters in floorplan files

## DAY 3:-

1) Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
2) Calculate the die area in microns from the values in floorplan def.
3) Load generated floorplan def in magic tool and explore the floorplan.
4) Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
5) Load generated placement def in magic tool and explore the placement.

```math
Area\ of\ die\ in\ microns = Die\ width\ in\ microns * Die\ height\ in\ microns
```

#### 1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

```bash
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```tcl
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Now we can run floorplan
run_floorplan
```

Screenshot of floorplan run

![Screenshot synthesis](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/7deda325-2ae8-4e98-aa71-7a54f5c34fcb)
![Screenshot floorplan](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/c1fe538f-c58f-46b9-9466-b0873a88eb6c)

