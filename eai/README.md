# Embodied AI


## Prerequisites

- Hardware: Embedded electronics, mechanics
- Software base:
    - ROS framework.
    - Sensing: 
        - direct: Video, Radar, IMU
        - comprehension: SLAM, object detection
    - Control: based control thoery (PID, robotics)
- Learning:
    - RL
    - Imitation learning
    - DL estimated Robotics

### Hardware
### Software

#### ROS Framework (Robot OS)

It is not actually an OS, but a conventions to standardize Robot abstraction.

In simple words, it regularize robot sensing and controlling into API topics communication such as:
- `/turtle1/cmd_vel`: A **Publisher** node can be initilized to send controls to this topic to control some part of the robot.
- `/turtle1/pose`: A **Subscriber** node can be initilized to receive status from this topic to know some status of some part of the robot.

Key idea: 
> To decouple the hardware implementation and manupulation from control and display.

In your ROS development, you will need to implement your own Simulation with ROS nodes to-be controlled or listened.

#### Sensing: Radar
- **Ultrasonic Radar**: return distance. 
- **MMW Radar**: return point clouds: {(x, y, z, v)}. v for velocity, represent the speed to point towards radar center.
- **LiDAR**: return point clouds: {(x, y, z, i)}. i for intensity, can be used to infere the material.
- **Depth Camera**: return RGB-D image: (width, height, depth, color) eg. ToF Camera
- Others
    - Pulse Doppler Radar
    - Structured Light Camera

#### Sensing: IMU
Return sensor physical status including but not limited to:
- Acceleration (x, y, z)
- Angular velocity (x, y, z)
- Orientation (x, y, z)
- Megnetic Field (B1, B2, B3)

#### Control: State-Space Modeling
Based on several science equations, the robotic(including electrocal) system can be described as
a special form of differential equation:

$$
\dot{x}(t) = A x(t) + B u(t)
$$
$$
y(t) = C x(t) + D u(t)
$$

This equation is well-studied and it is easy to get a nice control formula from this equation system.

#### Control: PID control

Control via PID formula:

$$
u(t) = K_p e(t) + K_i \int_0^t e(\tau) d\tau + K_d \frac{de(t)}{dt}
$$

$K_p$, $K_i$ and $K_d$ can somehow be figured out. Either emporalcally or calculated if State-Space Model is clear.


## Embodied Intelligence

Can be understood as highly level sensing (including deep understanding and reasoning, world rules modeling) 
and a more rational, target-specific, strategical motion control.  

The whole concept of embodied AI can be put into a RL framework, with following additional concepts:
- higher level perception of the environment.
- more reactive, complex and sophisticated goals build upon some core values.
- more realistic design of each parts of the algorithm facing towards real world.
- continuous learning and lifelong adjust and update of the model.
- evolve morphology design of the agent.
- emphasize generablilty.
- emphasize interpretability, more cautious.
- emphasize robustness.
- Trying to virtuous cycle of learning(perception) and doing(action).


### Simulated environment

Instead of learning from static datasets or directly from interactions in the full real world, 
Embodied AI primarily trains in simulated environments, 
either constrained real-world scenarios or fully virtual settings, 
with a strong emphasis on the latter—interactive virtual environments.

Just like `envs` in OpenAI gym. Those envs accept actions (of an agent) and return the state of env stepwise.
Compare to OpenAI gym, those envs usually contains image from the camera of the agent and the image tends to be photo realistic.
And the actions can be more detailed and map to complete controls of the robot agent.

for example:
- Gibson, focus on photo-realistic FPV, and refined segmentation.
- AI-Thon, focus on more complex iterations to the elements in the env. 

**Static datasets**
Some dataset are not interactive but contains annotated series of actions or trajectory. Those datasets can be used to:
- pretrain the model
- imitation learning
- offline RL


## Category

- Embodied Perception: Multi-modal
- Embodied Interation: eg. grasp, voice control
- Embodied Agents: mix perception and action, focus on planning.
- Sim2Real Adaption: focus on details of transfering robots from simulation to real world.


### Hip area

#### Joint learning of morphology and policy
Deep Evolutionary Reinforcement Learning (DERL)

#### Multi-task generation
- Multi-task RL
- Meta-Learning

#### Multi-modal perception

#### LLM-control

#### Bionic robot