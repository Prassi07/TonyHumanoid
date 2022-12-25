# TonyHumanoid
 Base Code for TonyHumanoid Robot

A 17 DOF Humanoid Robot created as part of the undergraduate Project as a research platform to test different algorithms for humanoid robot. The robot is capable of simple actions like walking and turning. New gaits can be generated using matlab trajectory sequences and the inverse kinematic function. The robot can be controlled serially using an bluetooth device.

Contributors:
1. Prasanna Sriganesh (https://prassi07.github.io)
2. Prajwal Rajendra Mahendrakar (https://scholar.google.com/citations?user=wZH3lt8AAAAJ&hl=en)

If using this code, please cite
"Prasanna Sriganesh, Prajwal Rajendra Mahendrakar and Rajasekar Mohan, “Solving inverse kinematics using geometric analysis for gait generation in small-sized humanoid robots,” in Proc. IEEE/SICE International Symposium on System Integration(SII), Honolulu, Hawaii, USA, 12th-15th  January 2020, pp. 384–389" 

You can check out the project on my website [here](https://prassi07.github.io/projects/tonyhumanoid)

The main code consists of three files, 4 other files are used for analysing data and are described below.

#### TonyGenerateTrajectories.m

Program which generates Angles of the Actuators for robots to walk forward using the 3-D LIP model

* Inputs	:  
	* Value of Time Period(T).
	* Value of Step Length L in mm.
	* Value of Step Height H in mm, 
    * Value of half of Pelvis Distance(K) in mm.
* Outputs :   
	* Doesnot return any value.
	* Creates a file "angles_generated.txt" consiting all the angles
	* Each line has 10 angles, first 5 are for right leg and other for left leg
        * Each 5 angles are for - Hip Roll, Hip Pitch, knee Pitch, Ankle Roll and Ankle Pitch

#### TonyIK.m

Function to Solve inverse kinematics of 5-dof leg of humanoind robot

* Inputs	:   
	* Foot Co-ordinates of the robot leg - xf,yf,zf
        * Hip Co-ordinates of the robot leg - x1,y1,z1
        * Character l or r, for left and right leg, only for displaying
            purposes
* Output	:   
	* Returns 5 angles - hip roll, hip pitch, knee pitch, ankle pitch, ankle roll

#### RunAngles.py

Python script to read the generated text file and send the angles to Tony humanoid via serial protocol

* Inputs	:   
	* Generated text file "angles_generated.txt" from above matlab script
* Outputs	:   
	* No outputs, sends angles to hardware via serial protocol

#### PlotAngles.m

Matlab script which reads the genrated txt file, and plots angles with respect to time step, useful to check abnormalities

* Inputs:	    
	* Generated text file "angles_generated.txt" from above matlab script
* Outputs	:   
	* Plots a graph of all angles with respect to time.

#### compute_dh_matrix.m

Function which generates the Denavit-Hartenberg Matrix for given parameters
* Inputs	:   
	* D-H parameter r
	* D-H parameter alpha
	* D-H parameter d
	* D-H parameter theta
* Outputs	:   
	* Returns D-H matrix A

#### transforms_init.m

Initialize Transforms matrix for the robot using the D-H matrix to be able to visualize the generated angles.
* The Tranforms are generated specifically for Tony's parameters, should be changed manually for other robots.

#### test_tranform+.m

Script which reads the generated angles, and visulizes the robot's pose using the generated transform matrices
* Inputs	:   
	* File "angles_generated.txt"
	* Initialized Transform Matirx
* Outputs	:   
	* A visualization of robot's links

#### angles_generated.txt

A sample file containing actuator angles for generated walk gait.
Each line of this file contains tab separted integer values. The first five values are the actuator angles for the right leg in the order Hip Roll, Hip Pitch, Knee Pitch, Ankle Pitch, Ankle Roll. The next five values are the actuator angles for the left leg in the exact same order as above.


To run the Source Code
---

* Step 1 : Open the file TonyGenerateTrajectories.m
* Step 2 : Set the robot parameters, Link Lengths (l1,l2,l3,l4,l5) in TonyIK.m
* Step 3 : Set the walk parameters , PelvisDistance, CoM plane height, Step Height H and Step Length(L) in TonyGenerateTrajectories.m 
* Step 4 : Invoke scirpt TonyGenerateTrajectories.m 
* Step 5 : This generates a angles_generated.txt file which contains the actuator angles of the robot's right and left leg. Each line of this file has 10 angles, first 5 for right leg and latter for the left leg. The conventions are shown above.
* Step 6: Use the generated txt file with RunAngles.py to send them to the robot(specific to Tony Robot)

Use other files to visualize and graph generated data.
