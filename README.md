Download Link: https://assignmentchef.com/product/solved-ivr-assignment-1
<br>
This assignment will be extending a lot of what was previously done in the labs to a non-planar (3D) robot with 4 degrees of freedom. You will be working in groups of two. There will be, however, no extra credit for completing the assignment alone. The assignment is going to be broken down into 2 sections that cover robot vision and control.

<h1>1           Overview of the Simulator</h1>

<h2>1.1         Installation of Lab Library</h2>

<ol>

 <li>Use UBUNTU as instructed in labs.</li>

 <li>Create a folder in your home directory, here we named the folder <strong>catkin ws</strong>, enter the folder and create another folder named <strong>src</strong>. You can do it via the terminal:</li>

</ol>

<h3>mkdir catkin ws cd catkin ws mkdir src</h3>

<ol start="3">

 <li>The package for the lab is in a repository (repo) on Github which you can find through the following link: <a href="https://github.com/AQQQQY/ivr_assignment.git">https://github.com/AQQQQY/ivr_assignment.git</a> You can download it, unzip, and put in a folder named <strong>ivr assignment </strong>inside the <strong>src </strong>folder you just created. <strong>Important: </strong>Make sure the folder that includes the downloaded files is named <strong>ivr </strong><strong>assignment </strong>and is inside the <strong>src </strong></li>

 <li>Get back to your workspace folder <strong>cd </strong>∼<strong>/catkin ws</strong>. Use the following command to install the package you just downloaded:</li>

</ol>

<h3>catkin make source devel/setup.bash</h3>

<strong>Important: </strong>The setup.bash file will have to be sourced as above in every new terminal. You can also add this to the end of your .bashrc file to automatically do it whenever a new terminal is opened. To do so you can open <strong>/.bashrc </strong>using <strong>gedit /.bashrc</strong>. Add the following two lines at the end of the opened file and save:

<h3>source /opt/ros/melodic/setup.bash source ∼/catkinws/devel/setup.bash</h3>

<ol start="5">

 <li>Once the installation is completed you can navigate to the ∼<strong>/catkinws/src/ivr assignment/src </strong>folder and run the following command to make the python files executable:</li>

</ol>

<h3>chmod +x image1.py image2.py</h3>

Note: If you create any python files in this folder you should make them executable using <strong>chmod </strong>command.

Once the installation is completed you can navigate to the ∼<strong>/catkin ws</strong>folder and run the robot simulator using:

Figure 1: The robot in Gazebo simulation environment.

This opens the simulated robot in ROS simulation environment. The robot has 4 degrees of freedom and moves in a 3D world. The joints of the robot are shown by green (joint 1), yellow (joint 2 &amp; 3), and blue (joint4) spheres. The red sphere is the robot end effector. Joint 1 is a revolute joint rotating around its z axis. Joint 2 and 3 are located at the yellow circle and are revolute joints moving around the drawn y and x axes, respectively. Joint 4 is a revolute joint rotating around the y axis. The table below gives a description for each link:

<table width="289">

 <tbody>

  <tr>

   <td width="42">Link</td>

   <td width="57">Length</td>

   <td width="94">Rotation axis</td>

   <td width="96">Joint location</td>

  </tr>

  <tr>

   <td width="42">1</td>

   <td width="57">4[m]</td>

   <td width="94">z</td>

   <td width="96">Green</td>

  </tr>

  <tr>

   <td width="42">2</td>

   <td width="57">0[m]</td>

   <td width="94">y</td>

   <td width="96">Yellow</td>

  </tr>

  <tr>

   <td width="42">3</td>

   <td width="57">3.2[m]</td>

   <td width="94">x</td>

   <td width="96">Yellow</td>

  </tr>

  <tr>

   <td width="42">4</td>

   <td width="57">2.8[m]</td>

   <td width="94">y</td>

   <td width="96">Blue</td>

  </tr>

 </tbody>

</table>

The robot is in position control mode. You can move the robot’s joints using the following command in anew terminal:

<h3>rostopic pub -1 /robot/joint1 position controller/command std msgs/Float64 “data: 1.0”</h3>

This line of code will move the joint 1 by 1 Radian. You can start to get familiar with the simulator by changing the joint angles. If you want to move another joint change the joint number in the above code. Joint 1 can be moved between −<em>π </em>and <em>π </em>and the rest of the joint can be moved between −<em>π/</em>2 and <em>π/</em>2.

The simulator is also designed to return two RGB arrays from two cameras placed around the robot. The images from the cameras are what you will be performing computer vision algorithms on.

The main codes which you shall use in the labs is inside ∼<strong>/catkin ws/src/ivr assignment/src </strong>and named <strong>image1.py </strong>and <strong>image2.py</strong>.

This codes receive the images from the cameras, process it and publish the results. To run the codes, open up a new terminal and use these commands:

<h3>rosrun ivr assignment image1.py</h3>

It should show the image received from camera 1.

<strong>rosrun ivr </strong><strong>assignment image2.py </strong>should show the image received from camera 2.

Try to move the robot and check if the robot moves in the camera views. You should modify these codes as you did in the labs.

<h1>2           Robot Vision</h1>

<h2>2.1         Joint state estimation – I</h2>

<h3>2.1.1         Problem statement</h3>

As part of the new simulation you are given two orthogonal views on the zy plane and the xz plane. Similar to the labs you will need to calculate the joint angles for the robot to use. For this part of the assignment assume joint 1 is fixed and robot can only move in a 3D world with 3 degree of freedom (DoF). Next, create a node to move the other three joints using the following sinusoidal signals:

joint2= joint3= joint4=

where <em>t </em>denotes the time in seconds.

This can be done by publishing to topic ”/robot/joint{x} position controller/command”, where ”{x}” is [2, 3, 4].

Create a python file named ”vision 1.py” in <strong>src </strong>folder, use it to start a node that estimates the value of the 3 joints using computer vision. You may use whichever technique you want. Note that some of the spheres might not be clearly visible in one camera when the robot moves in 3D. Your algorithm should be able to handle these scenarios.

In your report, describe your algorithm (5 marks) and provide 3 plots (each 4 marks). In each plot, you should compare the estimated value of one joint with the sinusoidal signal that you used to move the joint. The plot should show the estimated joint values for at least 15 seconds. When comparing your estimated values with the sinusoidal signal, please describle what you observe using serveral sentences and analysis the reason of the errors, especially relatively big errors in some time periods (3 marks) .

<h3>2.1.2         Expected outcome</h3>

By the end your system should be able to accurately acquire the joint states of the robot (average error less than 0.15 radian error).

To plot the results you can publish your estimated joints on a topic and use <strong>rqt plot </strong>command. We have used several codes in the labs to create a publisher and publish data. Check out the lab solutions if you don’t know how to do it. To plot two topics vs each other you can use <strong>rqt </strong><strong>plt [TOPIC1 </strong><strong>NAME] [TOPIC2 NAME]/data[num] </strong>use TOPIC1 NAME if the topic is only one number and [TOPIC2 NAME]/data[num] if the topic is an array.

To change the limits of rqt plot click on the arrow shaped button. Select a reasonable length to show the results, e.g. 15 seconds. You can save your plot by clicking on the save button. Additionally, you can record your data using <strong>rosbag record </strong>command and plot them in Python. See the following link for more information <a href="http://wiki.ros.org/rosbag/Code%20API#py_api">http://wiki.ros.org/rosbag/Code%20API#py_api</a>

<h2>2.2         Joint state estimation – II</h2>

Repeat the process described in section 2.1. This time do not fix joint 1, instead fix joint 2. Joint 1, 3 and 4 are free to move.

Similar to Section 2.1, create a node to move the joints using the following sinusoidal signals:

joint1= joint3= joint4=

where t denotes the time in seconds.

Create a python file named ”vision 2.py” in <strong>src </strong>folder, use it to start a node that estimates the value of the 3 joint angles using computer vision. You may use whichever technique you want. In your report, describe your algorithm (4 marks) and provide 3 plots (each 2 marks). In each plot, you should compare the estimated value of one joint with the sinusoidal signal that you used to move the joint. The plot should show the estimated joint values for at least 10 seconds.

<h1>3           Robot Control</h1>

Joint 2 will be frozen throughout this section. Joint 1, 3 and 4 are free to move.

<h2>3.1         Forward Kinematics</h2>

In this section we will be using the joint angle estimations you have obtained from Section 2.2, with joint 2 frozen. Calculate the equations for robot Forward Kinematics (FK). We are only interested in controlling the x,y, and z position of the robot end-effector. Ignore the end-effector’s orientation. The FK should look like this:

  <em>x<sub>e</sub></em>

<em>K</em>(<em>q</em>) = <em>y</em><em>e</em>                                                                                        (1)

  <em>z<sub>e</sub></em>

where <em>x<sub>e</sub></em>, <em>y<sub>e</sub></em>, <em>z<sub>e </sub></em>are the end-effector position and <em>q </em>= (<em>θ</em><sub>1</sub><em>,θ</em><sub>3</sub><em>,θ</em><sub>4</sub>).

Implement the FK in a new python file, ”control.py”. It should subscribe to topics published by ”vision 2.py”.

In your report, present the results of your Forward kinematics calculation (5 marks). To verify your FK using your code implementation, move the robot to 10 different points across it’s workspace using rostopic pub command. Do not keep any of the 3 joints zero while selecting these 10 points. Compare the estimated end-effector position via the images to the estimated end-effector position via FK in a table and comment on accuracy (5 marks).

<h2>3.2         Inverse Kinematics</h2>

From the previous tasks you can acquire an estimation of the joint states. Calculate the Jacobian of the robot.

Our topic named /target control/target pos will publish a target position for the robot end-effector at a frequency of 50Hz. Your task is to calculate the necessary rotation of the each joint, so that the end-effector reach the target position. In the ”control.py” you created in Section 3.1, develop a Controller similar to lab3 to follow the target position.

By the end, your robot should be moving to the target position. Not only this you should be able to report quantitatively the accuracy of the arm movement. Present the results of your inverse kinematics calculation (4 marks). Present three plots (2 marks for each) comparing the x,y, and z position of the robot end-effector with the x,y, and z position of the published target. The plot should show the positions for at least 20 seconds. The starting several seconds of your robot can be a random jiggly motion, you can ignore the motion and start your evaluation only after the robot converges to the target position.