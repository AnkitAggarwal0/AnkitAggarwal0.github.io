---
layout: page
title: Coffee Barista
description: A robot arm is tasked with pouring beads representing different coffee ingredients
img: assets/img/barista_cover.jpg
importance: 3
category: fun
---
<b>Team:</b> Ankit Aggarwal, Aayush Fadia, Shreya Shri Ragi, Swastik Mahapatra 

<p align="center">
<iframe width="500" height="500" src="https://www.youtube.com/embed/ttPAshS-jtE?si=UfeMbiLEElGvZBkN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
</p>

In a simulated coffee preparation environment, a robot arm is tasked with pouring beads representing different coffee ingredients (milk, coffee, foam, chocolate) into a cup based on user input for various coffee types (latte, americano, espresso). The system must:
- <b> Controlled Pouring: </b> Pour beads in a controlled manner to achieve precise ingredient ratios
- <b> Constrained Manipulation: </b> Pick and move ingredient cups containing beads without spilling
- <b> Obstacle Avoidance: </b> Avoid collisions with task apparatus while moving in the environment 

<h3> <b> Setup </b> </h3>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/barista_main.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
- RealSense Camera
- Weighing Scale
- 2 Ingredient Cups 
- Output Cup (Placed anywhere on scale)

<br>

<h3> <b> Methodology </b> </h3>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/barista_algo.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<h4> Perception </h4>
The major perception component of our project is to localize and check the output coffee cup.
1. Detect cup placed on the platform: Confirm if an output cup is present on the preparation platform from a set perceive pose.
1. Localize the rim of the cup: Transform the data to global map for planner.
1. Localize the cup in 3D space using depth data and determine its bounding cylinder (radius + depth).
1. Register the resultant cylinder to the collision space.

<h4> Motion Planning </h4>
Motion planning is divided into three phases - Grasp Ingredient Cup, Bring ingredient cup above Coffee Mug and Replace Ingredient Cup

1. <b> Grasp Ingredient Cup </b>
    - <b>Start: </b> Arm Home Configuration. 
    - <b>Goal: </b>Place fingers horizontal and around the cup.
    - <b>Obstacles to Avoid: </b>All objects on table - tray, cups, mug, scale, virtual walls, and arm itself.
    - <b>Approach: </b>Inform MoveIt about all obstacles (known/predefined and from perception). Allow MoveIt to plan and execute a path.

2. <b> Bring Ingredient Cup above Coffee Mug </b>
    - <b>Start: </b> End effector grasps Ingredient Cup in its original location.
    - <b>Goal: </b> Ingredient cup is directly above coffee mug.
    - <b>Constraints: </b> Keep cup vertical.
    - <b>Approach: </b> MoveIt plans a non-colliding, constraint respecting path.

3. <b> Replace Ingredient Cup </b>
    - <b> Start, Goal: </b> Reverse of Above.
    - <b> Constraints: </b> Same as above.
    - <b> Approach: </b> Plan a path via MoveIt to place ingredient cup back in original spot.

<h4> Pouring </h4>
Pouring beads in a controlled and precise manner requires robust and accurate feedback. 

1. <b> Feedback Method </b> 
    - A weighing scale will be used to weigh the amount of beads being poured into a cup. 
    - Fixed weight values will be defined as goals for the lookup table. 
1. <b> Lookup Table Method </b>
    - A lookup will be used to control the pouring with a focus on the amount of beads in the ingredient cup to select the correct angle to control flow rate to satisfy target pour amount. 
    - Weight of beads in the ingredient cup is obtained as feedback from the end effector’s force torque sensor
    - A control angle and offset weight will be defined for each ingredient cup weight range
1. <b> Manipulation using Control Values </b>
    - The control angle will used to create a goal pose of the end effector. 
    - The goal pose will be reached using inverse kinematics of the franka arm. 
    - The offset weight will be used as a stop condition for pouring to control over-pour.
