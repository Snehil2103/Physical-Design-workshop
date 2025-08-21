# Digital VLSI SoC Design and Planning of Picorv32

# Day 1: Inception of open-source EDA, OpenLANE and Sky130 PDK

Day1 Tasks:

  1. Run picorv32a design synthesis using OpenLANE flow and generate necessary outputs.
  2. Calculate the Flipflop ratio

1.Picorv32a design synthesis using OpenLANE

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

2. Flipflop ratio calculation

<img width="1284" height="770" alt="Screenshot 2025-08-11 182000" src="https://github.com/user-attachments/assets/0adac9df-3a81-4ac2-b627-71903e46f2db" />

<img width="1280" height="765" alt="Screenshot 2025-08-11 181852" src="https://github.com/user-attachments/assets/b488e42a-bcb5-4f94-b591-77a50ea1a98b" />

Ratio = 1613/14876 = 0.10

Percentage = Ratio * 100 = 10%


# Day2: Good floorplan vs Bad floorplan and Introduction to library cells

Day2 Tasks:-

  1. Run 'picorv32a' design floorplan using OpenLANE flow and generate necessary outputs.
  2. Load generated floorplan def in magic tool and explore the floorplan.
  3. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.
  4. Load generated placement def in magic tool and explore the placement.


1.Run Picorv32a design floorplan using OpenLANE flow and generate necessary outputs.

Commands to invoke the OpenLANE flow and perform floorplan

```
# Resume from synthesis stage
run_floorplan
```

<img width="1281" height="764" alt="Screenshot 2025-08-11 180943" src="https://github.com/user-attachments/assets/876ef230-060d-436a-bee3-4c184ad32b16" />


2. Load generated floorplan def in magic tool and explore the floorplan.

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


3. Run Picorv32a design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

```
#Resume from floorplan stage
run_placement
```

<img width="1283" height="770" alt="Screenshot 2025-08-11 181103" src="https://github.com/user-attachments/assets/dec6dc63-d802-4624-8c5d-fb0cd5d163ff" />

<img width="1283" height="772" alt="Screenshot 2025-08-11 181240" src="https://github.com/user-attachments/assets/2d408d31-2bcc-4647-b6ea-4f0e7bf30abb" />


4. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

```
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/11-08_12-36/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

<img width="1280" height="764" alt="Screenshot 2025-08-11 190949" src="https://github.com/user-attachments/assets/d286bd39-2107-4c9f-b8a8-fefa317232c5" />

<img width="1280" height="764" alt="Screenshot 2025-08-11 191124" src="https://github.com/user-attachments/assets/69a408ad-2332-4851-a710-ca57ab5970dc" />


# Day3: Design library cell using Magic Layout and ngspice characterization

Day3 Tasks:

  1. Load the custom inverter layout in magic and explore.
  2. Spice extraction of inverter in magic.
  3. Editing the spice model file for analysis through simulation.
  4. Post-layout NGSpice simulations.
  5. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

1.Load the custom inverter layout in magic and explore.


```
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

<img width="1280" height="766" alt="Screenshot 2025-08-11 192806" src="https://github.com/user-attachments/assets/8bda63c2-8124-4616-a250-a6bd671e7f3f" />

2. Spice extraction of inverter in magic tkcon window

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

```
# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
```

<img width="1282" height="767" alt="Screenshot 2025-08-11 193321" src="https://github.com/user-attachments/assets/b12e2b90-ecc2-4671-85d8-b8cdaa5f559e" />

Spice file:

<img width="1281" height="772" alt="Screenshot 2025-08-11 193507" src="https://github.com/user-attachments/assets/21220501-d97b-4b7d-a5b4-67d38b078637" />

3. Editing the spice model file for analysis through simulation

Edited file: 

<img width="1284" height="774" alt="Screenshot 2025-08-11 200459" src="https://github.com/user-attachments/assets/0e31d1e5-c7a8-4682-843f-b584c4ca093c" />

4. Post layout NGSpice simulations

Commands for ngspice simulation

```
# Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

# Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a
```

<img width="1287" height="773" alt="Screenshot 2025-08-11 201050" src="https://github.com/user-attachments/assets/ab69b660-721b-45fd-a245-a9f971e2667b" />

<img width="1279" height="767" alt="Screenshot 2025-08-11 201127" src="https://github.com/user-attachments/assets/31de7a13-f2fe-4633-a9b4-4e58404d5ff3" />

<img width="1280" height="768" alt="Screenshot 2025-08-11 205243" src="https://github.com/user-attachments/assets/f76a4bcf-29a6-4228-a4e0-dc2ffe26c8c6" />

From the above screenshot,

  Rise Transition time = Time taken by output to rise to 80% - Time taken by output to rise to 20%

  Rise Transition time = 2.23529 - 2.18289 = 0.05240 ns = 52.40 ps

  Rise Cell delay = Time taken by output to rise to 50% - Time taken by input to fall to 50%

  Rise Cell delay = 2.20726 - 2.14988 = 0.05738 ns = 57.38 ps

5. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

```
# Change to home directory
cd

# Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

# Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

# Change directory into the lab folder
cd drc_tests

# List all files and directories present in the current directory
ls -al

# Command to view .magicrc file
gvim .magicrc

# Command to open magic tool in better graphics
magic -d XR &
```

<img width="1286" height="767" alt="Screenshot 2025-08-11 210038" src="https://github.com/user-attachments/assets/94035c62-2daa-46f8-b5c3-e417078375b4" />

Incorrectly implemented poly.9 rule no drc violation even though spacing < 0.48u

<img width="1031" height="544" alt="Screenshot 2025-08-11 210214" src="https://github.com/user-attachments/assets/893b5036-bd68-4521-aff9-c528ca0b6a46" />

<img width="1033" height="546" alt="Screenshot 2025-08-11 210246" src="https://github.com/user-attachments/assets/b6d24050-a879-4498-becc-17004d098877" />

New commands inserted in sky130A.tech file to update drc

<img width="1280" height="765" alt="Screenshot 2025-08-11 211638" src="https://github.com/user-attachments/assets/2101c87d-3636-4c70-aa6f-7bd33d46bd04" />

Screenshot of magic window with rule implemented

<img width="1035" height="563" alt="Screenshot 2025-08-11 211744" src="https://github.com/user-attachments/assets/2a22185a-41da-4c5b-9f8b-f5d5bb749019" />

<img width="1036" height="559" alt="Screenshot 2025-08-11 211821" src="https://github.com/user-attachments/assets/9c194439-7155-4554-a336-19385daddc1c" />


# Day4 - Pre-layout timing analysis and importance of good clock tree

Day4 tasks:-

  1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.
  2. Save the finalized layout with custom name and generate lef
  3. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
  4. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
  5. Run openlane flow synthesis with newly inserted custom inverter cell.
  6. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
  7. Run floorplan and placement and verify the cell is accepted in PnR flow.
  8. Do Post-Synthesis timing analysis with OpenSTA tool.
  9. Perform Clock Tree Synthesis
  10. Post-CTS OpenROAD timing analysis.

1.Fix up small DRC errors and verify the design is ready to be inserted into our flow:

Conditions to be verified before moving forward with custom designed cell layout:

  Condition 1:  The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
  Condition 2:  Width of the standard cell should be odd multiples of the horizontal track pitch.
  Condition 3:  Height of the standard cell should be even multiples of the vertical track pitch.

```
# Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &
```

Screenshot of tracks.info of sky130_fd_sc_hd

<img width="1279" height="774" alt="Screenshot 2025-08-11 215943" src="https://github.com/user-attachments/assets/4a2e0412-d870-43c9-af7d-daed095c3ad4" />

Commands for tkcon window to set grid as tracks of locali layer

```
# Get syntax for grid command
help grid

# Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um
```

<img width="1279" height="765" alt="Screenshot 2025-08-12 105034" src="https://github.com/user-attachments/assets/cf2c8960-ccc9-4a05-b33d-59d1424b55bb" />

Condition 1 is verified

<img width="1281" height="766" alt="Screenshot 2025-08-12 105215" src="https://github.com/user-attachments/assets/ed4342b1-828a-4b06-a968-4a7e1ae0fad8" />

Condition 2 is verified

<img width="1475" height="773" alt="Screenshot 2025-08-12 105548" src="https://github.com/user-attachments/assets/986c929a-9617-4abe-bb89-9d79f2fe8e5b" />

Condition 3 is verified

<img width="1475" height="780" alt="Screenshot 2025-08-12 105646" src="https://github.com/user-attachments/assets/09c41a28-7d1c-4b85-b912-648fe9ba830e" />

2. Save the finalized layout with custom name and generate lef:

Command for tkcon window to save the layout with custom name

```
# Command to save as
save sky130_vsdinv.mag
```

Command to open the newly saved layout and generate lef

```
# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &

# lef command
lef write
```

<img width="1284" height="769" alt="Screenshot 2025-08-12 110033" src="https://github.com/user-attachments/assets/fb19bb2c-a61d-4272-8ebd-256fa6b64aec" />

Screenshot of newly created lef file

<img width="1282" height="765" alt="Screenshot 2025-08-12 110335" src="https://github.com/user-attachments/assets/eeb331ac-052e-4974-8e8b-718c280c8f04" />

3. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

```
# Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
```

4. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
 
Commands to be added to config.tcl to include our custom cell in the openlane flow

```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```

Edited config.tcl to include the added lef and change library to ones we added in src directory

<img width="1282" height="773" alt="Screenshot 2025-08-12 111112" src="https://github.com/user-attachments/assets/1c0998d3-12ae-4536-86e8-c0ff24abd0ed" />

5. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis

```
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```

```
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

<img width="1277" height="768" alt="Screenshot 2025-08-12 111319" src="https://github.com/user-attachments/assets/803be36e-fea8-4aa9-a77f-a809fcede0d0" />

<img width="1282" height="764" alt="Screenshot 2025-08-12 111445" src="https://github.com/user-attachments/assets/de59c072-7a26-4474-af73-1a232a93795a" />

<img width="1283" height="768" alt="Screenshot 2025-08-12 111623" src="https://github.com/user-attachments/assets/a1b19aa4-5457-4755-b3e8-f40e909af948" />

6. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing

<img width="1279" height="774" alt="Screenshot 2025-08-12 111704" src="https://github.com/user-attachments/assets/ac538f59-a141-4a99-9ac7-14b6a0a66e82" />

Commands to view and change parameters to improve timing and run synthesis

```
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 12-08_05-42 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

<img width="1273" height="764" alt="Screenshot 2025-08-12 113309" src="https://github.com/user-attachments/assets/1f95155c-b932-4742-97ab-d18e96b850cf" />

<img width="1284" height="766" alt="Screenshot 2025-08-12 112426" src="https://github.com/user-attachments/assets/676ada2d-ee37-463f-95e4-02b5c109761b" />

<img width="1284" height="767" alt="Screenshot 2025-08-12 112745" src="https://github.com/user-attachments/assets/49fac270-5e84-4f0d-bb2f-82af06bef41c" />

<img width="1278" height="772" alt="Screenshot 2025-08-12 112929" src="https://github.com/user-attachments/assets/17845c6e-adb4-4155-b223-38ae6c9a6bb3" />

<img width="1278" height="756" alt="Screenshot 2025-08-12 113000" src="https://github.com/user-attachments/assets/59edf5e4-bdc7-43de-9a66-b74241eb341a" />

7. Run floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following commands

```
# floorplan commands
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement
```

<img width="1281" height="770" alt="Screenshot 2025-08-12 114312" src="https://github.com/user-attachments/assets/e9bc4427-3887-4c9c-bc5f-931d375df297" />

<img width="1283" height="765" alt="Screenshot 2025-08-12 114355" src="https://github.com/user-attachments/assets/9f26eac3-5ffb-4172-b0b6-09502602a9c2" />

<img width="1282" height="771" alt="Screenshot 2025-08-12 114507" src="https://github.com/user-attachments/assets/0a0d168d-c5b7-4196-85c4-22468665062d" />

Commands to load placement def in magic in another terminal

```
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-08_05-42/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

<img width="1280" height="765" alt="Screenshot 2025-08-12 115630" src="https://github.com/user-attachments/assets/30600e8c-6cb9-4a49-9e99-5810fd177f68" />

We succesfully inserted our custom inverter

<img width="1282" height="770" alt="Screenshot 2025-08-12 115758" src="https://github.com/user-attachments/assets/38cf54ae-41c2-4b4e-bd06-517362b08506" />

Command for tkcon window to view internal layers of cells

```
# Command to view internal connectivity layers
expand
```

<img width="1283" height="764" alt="Screenshot 2025-08-12 115937" src="https://github.com/user-attachments/assets/662635a3-01d1-4cd9-8bf0-e3630c9ddd6a" />

8. Do Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis

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

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

Newly created pre_sta.conf for STA analysis in openlane directory

<img width="1277" height="766" alt="Screenshot 2025-08-12 150731" src="https://github.com/user-attachments/assets/731d0f4d-2b9d-40b3-8458-c789b7a26df0" />

Newly created my_base.sdc for STA analysis in openlane/designs/picorv32a/src directory based on the file openlane/scripts/base.sdc

<img width="1283" height="769" alt="Screenshot 2025-08-12 145942" src="https://github.com/user-attachments/assets/7113d55f-649e-490a-a4a5-2715e66a2299" />

Commands to run STA in another terminal

```
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```

<img width="1280" height="769" alt="Screenshot 2025-08-12 151836" src="https://github.com/user-attachments/assets/30fa44c9-6f38-4b22-9e1e-b5c34982f538" />

The slack is positive

9. Run Clock Tree Synthesis

```
# With placement done we are now ready to run CTS
run_cts
```

<img width="1282" height="753" alt="Screenshot 2025-08-12 153332" src="https://github.com/user-attachments/assets/4db9fffe-118a-4991-ae4a-364dbe816e11" />

<img width="1279" height="768" alt="Screenshot 2025-08-12 153407" src="https://github.com/user-attachments/assets/08c7719c-74b7-42d8-a40f-de6ffa3fe2dc" />

10. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/12-08_10-17/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/12-08_10-17/results/cts/picorv32a.cts.def

# Creating an OpenROAD database to work with
write_db pico_cts.db

# Loading the created database in OpenROAD
read_db pico_cts.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/12-08_10-17/results/synthesis/picorv32a.synthesis_cts.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

```

<img width="1278" height="761" alt="Screenshot 2025-08-12 154306" src="https://github.com/user-attachments/assets/b4bfdaf6-4ce9-46be-9fdf-4a8417af0225" />

<img width="1281" height="765" alt="Screenshot 2025-08-12 154328" src="https://github.com/user-attachments/assets/a8d8898e-61bd-4e93-8e23-43f73033f1be" />


# Day 5 - Final steps for RTL2GDS using tritonRoute and openSTA

Day5 tasks:-

   1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
   2. Perfrom detailed routing using TritonRoute.
   3. Post-Route parasitic extraction using SPEF extractor.
   4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.


1.Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
```
# Now that CTS is done we can do power distribution network
gen_pdn
```

<img width="1281" height="762" alt="Screenshot 2025-08-12 155347" src="https://github.com/user-attachments/assets/32cc162c-6a17-483a-bb59-282b4c34f75b" />

<img width="1281" height="759" alt="Screenshot 2025-08-12 155419" src="https://github.com/user-attachments/assets/71a5cb50-4307-47ff-b7c1-b73382df989d" />

Commands to load PDN def in magic in another terminal

```
# Change directory to path containing generated PDN def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-08_10-17/tmp/floorplan/

# Command to load the PDN def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
```

<img width="1034" height="553" alt="Screenshot 2025-08-12 155918" src="https://github.com/user-attachments/assets/0ae56c30-5f88-4cc1-aa9b-7fa96a228e91" />

<img width="1033" height="550" alt="Screenshot 2025-08-12 155942" src="https://github.com/user-attachments/assets/65f2d610-e664-4fe1-acda-89aabadf6fff" />

<img width="1031" height="548" alt="Screenshot 2025-08-12 160003" src="https://github.com/user-attachments/assets/ad35bea7-06cf-4a2c-acff-e59712bc1adf" />

2. Perfrom detailed routing using TritonRoute and explore the routed layout.

Command to perform routing

```
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
```

<img width="1275" height="761" alt="Screenshot 2025-08-12 161120" src="https://github.com/user-attachments/assets/9b44e4aa-01ad-4a0e-ae59-49a3c1bf7b2b" />

Commands to load routed def in magic in another terminal

```
# Change directory to path containing routed def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-08_10-17/results/routing/

# Command to load the routed def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &
```

<img width="1275" height="761" alt="Screenshot 2025-08-12 161434" src="https://github.com/user-attachments/assets/900fe953-aa80-40e0-862d-3fd93ae4292f" />

<img width="1285" height="769" alt="Screenshot 2025-08-12 161535" src="https://github.com/user-attachments/assets/62c8f5c0-670b-418b-b448-87de3ebaa8d3" />

3. Post-Route parasitic extraction using SPEF extractor.

Commands for SPEF extraction using external tool

```
# Change directory
cd Desktop/work/tools/SPEF_EXTRACTOR

# Command extract spef
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-08_10-17/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.def
```

4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD

```
# Command to run OpenROAD tool
openroad

# Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/12-08_10-17/tmp/merged.lef

# Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/12-08_10-17/results/routing/picorv32a.def

# Creating an OpenROAD database to work with
write_db pico_route.db

# Loading the created database in OpenROAD
read_db pico_route.db

# Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/12-08_10-17/results/synthesis/picorv32a.synthesis_preroute.v

# Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

# Link design and library
link_design picorv32a

# Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

# Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

# Read SPEF
read_spef /openLANE_flow/designs/picorv32a/runs/12-08_10-17/results/routing/picorv32a.spef

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
```

<img width="1000" height="319" alt="Screenshot 2025-08-12 163919" src="https://github.com/user-attachments/assets/479320a7-ee9e-4936-9023-34c1303f598d" />

<img width="1000" height="532" alt="Screenshot 2025-08-12 164111" src="https://github.com/user-attachments/assets/7fda92b6-6bc1-4b0f-b624-d9d8fc609c35" />

<img width="992" height="503" alt="Screenshot 2025-08-12 164136" src="https://github.com/user-attachments/assets/41bffd53-ba70-46b9-9591-1455c8a3e1d7" />

# Acknowledgement:

   I extend my sincere gratitude to Kunal Ghosh and the VSD team for their guidance.

 # Certificate of completion: 

 <img width="1404" height="983" alt="Screenshot 2025-08-21 225127" src="https://github.com/user-attachments/assets/e3a0b420-6db6-45eb-87b8-c0c48011b926" />















