# SOC_Design_and_planning_NASSCOM_VSD
### Implementation

#### The synthesis of a design picorv32a is processed in this step, a design with a default time period of 20ns and some sdc constraints, a verilog RTL, a clock port as shown as below:

Section 1 tasks:- 
1. Run 'picorv32a' design synthesis using OpenLANE flow and generate necessary outputs.
2. Calculate the flop ratio.

```math
Flop\ Ratio = \frac{Number\ of\ D\ Flip\ Flops}{Total\ Number\ of\ Cells}
```
```math
Percentage\ of\ DFF's = Flop\ Ratio * 100
```

* All section 1 logs, reports and results can be found in following run folder:

[Section 1 Run - 15-03_15-51](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/tree/main/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/15-03_15-51)

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

Screenshots of running each commands

![1](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/d19f6d0f-16f8-4e79-aa5a-f2a34b9fb203)
![2](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/5e03c8ca-8c7f-4579-a7bc-10161007910e)
![3](https://github.com/fayizferosh/soc-design-and-planning-nasscom-vsd/assets/63997454/5f196a31-059e-4192-a208-8a15ba1a0dd7)
