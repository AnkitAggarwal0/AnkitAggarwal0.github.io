---
layout: about
title: about
permalink: /
subtitle: Robotics Engineer | CMU Robotics Institute | AI + Mechatronics + Leadership

profile:
  align: right
  image: prof_pic.jpg
  image_circular: false # crops the image to make it circular
  more_info: >
    <p>Carnegie Mellon University</p>
    <p>Pittsburgh, PA</p>

news: false # includes a list of news items
selected_papers: false # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page
---

I architect autonomous systems designed to thrive where traditional engineering fails: unpredictable, unstructured, and extreme environments. From my time leading Mars Rover Manipal to delivering the Lunar ROADSTER at Carnegie Mellon, my path has been defined by a from-scratch philosophy. I bridge the gap between high-level intelligence and rugged physical execution. I enjoy the challenge of working across the entire robotics stack ranging from deriving the mathematical foundations for a deep neural network to prototyping custom cycloidal gearboxes to ensure hardware resilience.


I thrive in the 0-to-1 phase of robotics,  taking a complex, multidisciplinary problem and building a robust, field-ready solution. I am currently seeking Founding Robotics Engineer or early-stage technical roles where I can own the end-to-end development of complex systems and work across the robotics stack.

## Technical Skills

I am a full-stack engineer capable of owning a project from the mathematical derivation of a control law to the physical fabrication of the chassis.


#### The Brains: Autonomy, Controls, and Planning
* **Motion Planning:** Proficient in search-based (A*, Dijkstra) and sampling-based (RRT*, PRM) planners. Experienced in lattice-based planning and navigation in unstructured off-road environments.
* **Control Theory:** Expertise in PID, Model Predictive Control (MPC), and Inverse Kinematics (IK). Skilled in trajectory optimization and state estimation for high-degree-of-freedom manipulators.
* **Robotics Foundations:** Deep understanding of rigid body dynamics, spatial transformations, and physics-based simulation using Isaac Sim and MuJoCo.
* **Machine Learning for Robotics:** Utilizing CMU 11-785 and 10-601 foundations to integrate deep learning into the robotics stack, specifically for perception-based navigation and reinforcement learning (DAgger).
* **Industrial Automation:** Overhauled FANUC ArcMate workflows using KAREL and ROS-I, achieving over 90 percent repeatability and a 90 percent reduction in setup time.

#### The Body: Mechatronics and Hardware
* **Precision Mechanical Design:** SolidWorks Professional (CSWP) certified. Specialized in custom cycloidal gearbox design, tendon-driven systems, and mechanical logic elements for reliable control.
* **Embedded Development:** HAL/LL/Register-level programming for STM32 and TI Launchpad. Skilled in real-time firmware (C/C++), low-latency communication (SPI, I2C, CAN, UART), and industrial PLC interfacing via Python RPCs.
* **Power and Fabrication:** Integration of BLDC actuators, motor drivers, and battery management systems. Experienced in 3D printing for mechanical assemblies and hardware-in-the-loop (HIL) testing.
* **Circuit and PCB Design:** Expertise in schematic capture and PCB layout for sensor interfacing and power distribution. Proficient in component selection, mixed-signal systems, and rapid prototyping of custom breakout boards.


<h4> Find my complete CV <a href ="/cv"> here </a>. </h4>


<!--Write your biography here. Tell the world about yourself. Link to your favorite [subreddit](http://reddit.com). You can put a picture in, too. The code is already in, just name your picture `prof_pic.jpg` and put it in the `img/` folder.

Put your address / P.O. box / other info right below your picture. You can also disable any of these elements by editing `profile` property of the YAML header of your `_pages/about.md`. Edit `_bibliography/papers.bib` and Jekyll will render your [publications page](/al-folio/publications/) automatically.

Link to your social media connections, too. This theme is set up to use [Font Awesome icons](https://fontawesome.com/) and [Academicons](https://jpswalsh.github.io/academicons/), like the ones below. Add your Facebook, Twitter, LinkedIn, Google Scholar, or just disable all of them. -->
<br />

<h3> <b> <a href = "/projects"> Projects </a></b> </h3>
<hr>

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>


<br />

<h3> <b> Publications </b> </h3>
<!-- {% include bib_search.liquid %} -->
<div class="publications">

{% bibliography %}

</div>