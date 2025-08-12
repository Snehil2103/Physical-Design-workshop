# Digital VLSI SoC Design and Planning of Picorv32

# Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK

#Implementation

Day1 Tasks:

  1. Run picorv32a design synthesis using OpenLANE flow and generate necessary outputs.
  2. Calculate the Flipflop ratio

     Fliplop ratio = Number of D-Flipflops/Total number of cells


#Picorv32a design synthesis using OpenLANE

Commands to invoke the OpenLANE flow to perform synthesis

```
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit
```
<img width="1903" height="936" alt="Screenshot 2025-08-11 175140" src="https://github.com/user-attachments/assets/77db7d72-4328-4789-8251-f25893852711" />

<img width="1285" height="771" alt="Screenshot 2025-08-11 180732" src="https://github.com/user-attachments/assets/4b0200ba-3e83-4761-bb40-5a71d6bcf963" />

Flipflop ratio calculation

<img width="1284" height="770" alt="Screenshot 2025-08-11 182000" src="https://github.com/user-attachments/assets/0adac9df-3a81-4ac2-b627-71903e46f2db" />

<img width="1280" height="765" alt="Screenshot 2025-08-11 181852" src="https://github.com/user-attachments/assets/b488e42a-bcb5-4f94-b591-77a50ea1a98b" />

Ratio = 1613/14876 = 0.10

Percentage = Ratio * 100 = 10%


# Day2: Good floorplan vs Bad floorplan and Introduction to library cells

Section 2 tasks:-

  1.Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
  2.Calculate the die area in microns from the values in floorplan def.
  3.Load generated floorplan def in magic tool and explore the floorplan.
  4.Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
  5.Load generated placement def in magic tool and explore the placement.

    Area of die = Die width * Die height (in microns)
















