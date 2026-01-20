---
layout: page
title: Dexterous Bimanual and Humanoid Manipulation
description: Adapting Object-Centric Policies from Dual-Arm Systems to Humanoid Embodiments
img: assets/img/hands_1.png
importance: 1
category: research
---

<b> Team: </b> Ankit Aggarwal, Parth Gupta, Swastik Mahaptra, Joshua Pen, Deepam Ameria, Shreya Shri Ragi, Srishti Gupta\
<b> Role: </b> Robotics Engineer 

This research investigates the challenge of enabling robotic systems to match human-like adaptability in unstructured environments. We developed a hierarchical, vision-driven control framework that decomposes complex manipulation into a high-level wrist planner and a low-level reinforcement learning (RL) controller. A primary focus of this work was evaluating the "embodiment gap"—testing whether object-centric policies trained on fixed-base arms can generalize to humanoid platforms like the Unitree G1.

### **Hierarchical Framework Overview**
<hr>
The system leverages an object-centric formulation, reasoning in task space rather than specific joint space to theoretically enable "write once, run anywhere" capabilities.

1.  **High-Level Wrist Planner:** A Transformer-based generative policy that predicts 6-DOF wrist trajectories directly from monocular RGB image observations.
2.  **Low-Level Finger Controller:** An RL policy trained in Isaac Gym that translates reference trajectories into joint-level actions for stable object interaction.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/hierarchy.png" title="Policy Training and Testing Methodology" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<br>

## **Key Contributions & Extensions**

### **Transformer-Based Decoder**
We replaced the standard MLP-based decoders in the baseline ArcticNet architecture with a Transformer-based decoder. This design introduces learnable query embeddings and multi-head attention, allowing the model to reason over structured hand-object relationships rather than treating parameter regression as an unstructured mapping.

### **Embodiment Transfer to Unitree G1**
To bridge the gap between high-DOF Shadow Hands and the underactuated Inspire Hands of the Unitree G1, we implemented an explicit geometric mapping. 
* **Geometric Retargeting:** Forward kinematics were used to compute embodiment-independent fingertip positions in Cartesian coordinates.
* **Kinematic Mapping:** We solved for finger flexion angles (alpha) and thumb rotation (beta) to respect the reduced kinematic complexity of the humanoid platform.

### **PPO Optimization & Scalability**
We utilized Proximal Policy Optimization (PPO) with N=2048 parallel environments to stabilize high-variance gradient estimates. Our optimized configuration achieved a completion rate of 87.77%, exceeding the original Obj-Dex benchmark of 86.1%.

<br>

## **Results & Analysis**
<hr>
Our experiments demonstrated that while the high-level object-centric representation is transferable, the low-level execution requires embodiment-aware adaptation.

#### **Quantitative Comparison (Transformer vs. Baseline)**

| Metric | ArcticNet-SF (Baseline) | Transformer Decoder (Ours) |
| :--- | :--- | :--- |
| **Avg. MPJPE (mm)** | 53.37 mm | **50.69 mm** |
| **Avg. Success Rate** | 1.44% | **7.65%** |
| **Waffle Iron Success** | 2.01% | **19.17%** |

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/humanoid_imitation.png" title="Humanoid Policy Imitation" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<br>

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/hands_1.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/hands_2.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/hands_3.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/hands_4.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<br>

### **Ablation Study: PPO Stability**
The study confirmed that adaptive exploration enabled by learnable variance (Sigma) is critical for fine-grained control.

| Ablation | Horizon Length | Fixed Sigma | Completion Rate |
| :--- | :--- | :--- | :--- |
| 1 | 8 | True | 66.38% |
| 2 | 32 | True | 82.12% |
| **3 (Optimized)** | **8** | **False** | **87.77%** |

<br>

## **Technical Stack**
* **Simulators:** Isaac Gym (parallelized rollouts), MuJoCo (motion fidelity), and Isaac Lab.
* **Architectures:** ResNet-152 backbone, Transformer decoders, and shared MLP [1024, 512, 256] Actor-Critic networks.
* **Dataset:** ARCTIC bimanual hand-object interaction dataset.

<br>

## **Video Presentation**

<iframe width="800" height="600" src="https://www.youtube.com/embed/cUOIsDiRZcQ?si=UfeMbiLEElGvZBkN" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
