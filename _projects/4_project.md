---
layout: page
title: Automated Additive Manufacturing in Laser Welding Cell
description: Manufacturing Futures Institute, Carnegie Mellon University
img: assets/img/mfi.png
importance: 1
category: 
---
<b> Role: </b> Industrial Robotics Intern 

<b> Responsibilities </b> \
Creation of a ROS-Industrial Interface for Fanuc and ABB Robot Arms \
Application: Lincoln Electric Classmate Laser – DXF Pipeline for Additive Manufacturing

<h3> <b> DXF Pipeline for Additive Manufacturing </b></h3>
<hr>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/MFI.png" title="DXF File" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/mfi.png" title="Welding Process" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/mfi_weld.jpg" title="Weld Output" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    <b>Left:</b> Input DXF File |
    <b>Middle:</b> Lincoln Electric Classmater Welding Process |
    <b>Right:</b> Weld Output
</div>

1. DXF is created and stored 
1. DXF is called by the working script and parsed into robot poses using ezdxf 
1. The poses have a fixed z height and end effector orientation as this is a 2D demonstration 
1. The ROS interface and Welder class are launched 
1. The Laser is armed and starts emitting; Welding begins using comet_rpc 
1. ExecuteCartesianTrajectory service is used to send the rectangle trajectory to the robot and it executes  
1. Laser is disarmed and welding ends 

<b>Website:</b> <a href = "https://cmu-mfi.github.io/testbed/tutorials/le_classmate/le_classmate.html"> LE Classmate ROS </a>

<h4> <b> Additive Manufacturing Process </b> </h4>
<hr>

<iframe width="840" height="840" src="https://www.youtube.com/embed/Izd-oDhlwkU?si=UfeMbiLEElGvZBkN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>

<h3> <b> Custom ROS-Industrial Interface </b> </h3>
<hr>

<iframe width="840" height="473" src="https://www.youtube.com/embed/ci2d9Apd90k?si=UfeMbiLEElGvZBkN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<br>
<h4> Features </h4>
Interactive Digital Twin - allows moving/observing the robot using a GUI \
Broadens scope beyond robot-specific programming - robot can be programmed in both Python and C++ \
Custom ROS Services allow for trajectory execution with specifications using reliable path planners (Pilz, OMPL, CHOMP) 
- Go to a goal point
- Follow a trajectory (multiple goal points) 
- Follow a trajectory in a cartesian path

<h4> Keyence PLC I/O Control </h4>
The ROS interface provides services and topics, interfaced using comet_rpc, to enable I/O control. \
All I/O states are polled and published periodically on topics 
- /io_states_AIN - Analog Input Pins  
- /io_states_AOUT - Analog Output Pins
- /io_states_DIN - Digital Input Pins 
- /io_states_DOUT - Digital Output Pins 

ROS Services to access I/Os 
- /set_io_value - allows setting of all types of I/Os (analog/digital)
- /read_io_value - allows reading of all types of I/Os (analog/digital)
Hence, all peripheral devices connected to Fanuc I/Os can be controlled using the ROS interface and comet_rpc has been abstracted


<h4> Project Impact </h4>

| Before | After |
|---|---|
| Only structured text and teach pendant programming | Familiar languages - Python / C++ |
| Trajectories have to be manually taught by jogging the robot | Trajectories can be generated using MoveIt |
| No inputs supported | Complex Inputs Supported |
| No GUI or robot state feedback | Interactive GUI with real-time feedback |
| Robot could only be controlled by teach pendant | Robot can be controlled using GUI, user code and CLI |

<br>
<h4> Project Links </h4>
<b> Website: </b> <a href = "https://cmu-mfi.github.io/testbed/tutorials/fanuc_ros1/fanuc_ros1.html"> Fanuc ROS1 </a> \
<b> GitHub: </b> <a href = "https://github.com/cmu-mfi/fanuc_ros1"> fanuc_ros1 </a>
