# Digital VLSI SoC Design and Planning of Picorv32

# Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK

#Implementation

Day1 Tasks:

  1. Run picorv32a design synthesis using OpenLANE flow and generate necessary outputs.
  2. Calculate the Flipflop ratio

     Fliplop ratio = Number of D-Flipflops/Total number of cells


#Picorv32a design synthesis using OpenLANE

Commands to invoke the OpenLANE flow to perform synthesis

```# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker```
