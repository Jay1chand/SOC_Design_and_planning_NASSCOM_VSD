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
#open terminal in desktop
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

![Screenshot synthesis](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20105859.png)
![Screenshot floorplan](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20110003.png)

#### 2. Calculate the die area in microns from the values in floorplan def.

Screenshot of contents of floorplan def

![Screenshot floorplancont](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20112340.png)

results format:
UNITS DISTANCE MICRONS 1000 ;
DIEAREA ( 0 0 ) ( 660685 671405 ) ;

According to floorplan def
```math
1000\ Unit\ Distance = 1\ Micron
```
```math
Die\ width\ in\ unit\ distance = 660685 - 0 = 660685
```
```math
Die\ height\ in\ unit\ distance = 671405 - 0 = 671405
```
```math
Distance\ in\ microns = \frac{Value\ in\ Unit\ Distance}{1000}
```
```math
Die\ width\ in\ microns = \frac{660685}{1000} = 660.685\ Microns
```
```math
Die\ height\ in\ microns = \frac{671405}{1000} = 671.405\ Microns
```
```math
Area\ of\ die\ in\ microns = 660.685 * 671.405 = 443587.212425\ Square\ Microns
```
#### 3. Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```bash
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

```
Screenshots of floorplan def in magic

![Screenshot floorplan magic sim](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20112820.png)

#### 4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```tcl
# Congestion aware placement by default
run_placement
```

Screenshots of placement run

![Screenshot placementrun](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20120104.png)
![Screenshot from placementrun](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20120127.png)


#### 5. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

```bash
# Change directory to path containing generated placement def
cd /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/02-08_05-27/results/placement
# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshots of floorplan def in magic

![Screenshot from floorplan def](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20120545.png)
Standard cells legally placed 

![Screenshot from floorplan def zoomed standard cells](https://github.com/Jay1chand/SOC_Design_and_planning_NASSCOM_VSD/blob/main/Screenshot%202025-08-02%20120633.png)

Commands to exit from current run

```tcl
# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```

[Section 2 Run](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06)

### summary
1)completed floorplanning and placement according to requirements
2)optimized placement during run automatically matching signal integrity and timing constraints.

## DAY 4 - Design library cell using Magic Layout and ngspice characterization:- 

### Theory

### Implementation

* Section 3 tasks:-
1. Clone custom inverter standard cell design from github repository: [Standard cell design and characterization using OpenLANE flow](https://github.com/nickson-jose/vsdstdcelldesign).
2. Load the custom inverter layout in magic and explore.
3. Spice extraction of inverter in magic.
4. Editing the spice model file for analysis through simulation.
5. Post-layout ngspice simulations.
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.






