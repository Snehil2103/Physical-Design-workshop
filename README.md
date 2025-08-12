# Digital VLSI SoC Design and Planning of Picorv32

# Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK

# Implementation

Day1 Tasks:

  1. Run picorv32a design synthesis using OpenLANE flow and generate necessary outputs.
  2. Calculate the Flipflop ratio

     Fliplop ratio = Number of D-Flipflops/Total number of cells


# Picorv32a design synthesis using OpenLANE

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
```

<img width="1903" height="936" alt="Screenshot 2025-08-11 175140" src="https://github.com/user-attachments/assets/77db7d72-4328-4789-8251-f25893852711" />

<img width="1285" height="771" alt="Screenshot 2025-08-11 180732" src="https://github.com/user-attachments/assets/4b0200ba-3e83-4761-bb40-5a71d6bcf963" />

Flipflop ratio calculation

<img width="1284" height="770" alt="Screenshot 2025-08-11 182000" src="https://github.com/user-attachments/assets/0adac9df-3a81-4ac2-b627-71903e46f2db" />

<img width="1280" height="765" alt="Screenshot 2025-08-11 181852" src="https://github.com/user-attachments/assets/b488e42a-bcb5-4f94-b591-77a50ea1a98b" />

Ratio = 1613/14876 = 0.10

Percentage = Ratio * 100 = 10%


# Day2: Good floorplan vs Bad floorplan and Introduction to library cells

Day2 Tasks:-

  1.Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
  2.Load generated floorplan def in magic tool and explore the floorplan.
  3.Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
  4.Load generated placement def in magic tool and explore the placement.

# 1.Run Picorv32a design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

```
# Resume from synthesis stage
run_floorplan
```

<img width="1281" height="764" alt="Screenshot 2025-08-11 180943" src="https://github.com/user-attachments/assets/876ef230-060d-436a-bee3-4c184ad32b16" />

# 2.Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

```
# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-08_12-36/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

Floorplan view in Magic

<img width="1280" height="771" alt="Screenshot 2025-08-11 184017" src="https://github.com/user-attachments/assets/d93d5fdf-365f-45ad-ae13-d6c5de195593" />

Equidistant IO Ports 

<img width="1281" height="768" alt="Screenshot 2025-08-11 185449" src="https://github.com/user-attachments/assets/813eaa3f-3cdf-430f-9439-eb6670f31780" />

Diagonally placed Tap cells

<img width="1281" height="768" alt="Screenshot 2025-08-11 191325" src="https://github.com/user-attachments/assets/4a427dbe-bd25-4400-b880-8459d4825bbf" />

Unplaced Standard cells

<img width="1279" height="774" alt="Screenshot 2025-08-11 191640" src="https://github.com/user-attachments/assets/692fd985-9008-4c4d-b3e2-0e2ebc904527" />

Description of selected cell in tkcon window

<img width="1280" height="768" alt="Screenshot 2025-08-11 190704" src="https://github.com/user-attachments/assets/1afaebce-7645-4daf-86ec-86595fb0c0cc" />

# 3.Run Picorv32a design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```
#Resume from floorplan stage
run_placement
```

<img width="1283" height="770" alt="Screenshot 2025-08-11 181103" src="https://github.com/user-attachments/assets/dec6dc63-d802-4624-8c5d-fb0cd5d163ff" />

<img width="1283" height="772" alt="Screenshot 2025-08-11 181240" src="https://github.com/user-attachments/assets/2d408d31-2bcc-4647-b6ea-4f0e7bf30abb" />

# 4.Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

```
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-08_12-36/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
<img width="1280" height="764" alt="Screenshot 2025-08-11 190949" src="https://github.com/user-attachments/assets/d286bd39-2107-4c9f-b8a8-fefa317232c5" />

<img width="1280" height="764" alt="Screenshot 2025-08-11 191124" src="https://github.com/user-attachments/assets/69a408ad-2332-4851-a710-ca57ab5970dc" />




