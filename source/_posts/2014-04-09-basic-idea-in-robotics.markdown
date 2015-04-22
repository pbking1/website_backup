---
layout: post
title: "Basic idea in robotics"
date: 2014-04-09 18:55:54 +0800
comments: true
categories: Robot
keywords: robot

---

###ABSTRACT:
- The basic idea in robotic area
	- A robot is an autonomous system which exists in the physical world, can sense its environment , and can act on it to achieve some goals
	- The robotic involves autonomy, sensing, action, and achieving goals, all in the physical world
	- The component of the robot are 
		- physical body
			- it can exist and do in the physical world
		- combine 
			- manipulation(up body) 
				- handling objects
			- locomotion(down body).
				- Moving around, going places
	- Sensors
		- It can sense/perceive its environment in order to get information about itself and its surroundings.
	- Effectors and actuators
		- it can take actions
		- effector enable a robot to take a action, to do physical things
			- it can also be defined as any device that has an effect on the environment
			- it range from legs, wheels to arms and fingers
		- actuator can do exact the actual work for the robot 
			- are the effector that use underlying mechanism, such as motor and muscles.
			- Is also the mechanism that enable the effector to execute an action or movement
			- Such as electric motors(base on electric current), hydraulics(base on fluid pressure) ,pneumatics(base on air pressure) and photo-reactive materials ……
	- Controller
		- it can be autonomous
		- provide hardware and/or software that make the robot autonomous by using the sensor inputs and any other information to decide what to do ad then to control the effectors to execute that action
<!--more-->
###Some useful info about ATLAS robot
- 1.ATLAS robot has 27 total degrees of freedom.

- 2.ATLAS has 27 powerful actuators. They are very strong.
	- And they are using the Hydraulic Actuator

- 3.Even though ATLAS uses hydraulic actuators, the robot still uses gears. And 
	- it is possible to have backlash if you use hydraulic actuators.
	- And the backlash means any looseness between meshing gears
- 4.ATLAS robot27 joints are rotational. 
	- And they use position control, torque control and PID control.

- 5.ATLAS arms have 7 DOF. This means that manipulator is redundant. 
	- The controllable degrees of freedom > total degrees of freedom

- 6.Hands and feet are the end-effectors of the robot.

- 7.drive:
	- ATLAS need to detect depth through vision. Is stereopsis desired? True

- 8.In order to ATLAS to be able to detect LANES on a road, Edge detection might be most useful

- 9.walk:
	- if one leg (angle, knee and hip) has 4 DOF, and four PID controller needs to control the motion of the leg.

- 10.clear the way
	- compliance would not be beneficial in removing blocks to protect the robot from being hurt.
	- Torque control is the control method used to grab the door handle firmly
	- When open a door, we can choose Robustness to optimize path planning trajectories.

- 11.climb ladder
	- In order for robots to be successful in the real world they need to deal with uncertainty.
	- Programming robots to do the same thing over and over does not work in real environments. Instead they need to be able to generalize.
	- In the scenario, there are multiple ways in which ATLAS could coordinate the motion between his arms and legs. One coordination scheme for climbing could be the alternating gait(the way of walking)

- 12.pip detection
	- Laser-range scanner to compute distance is the most useful in helping the robot move through the building and find the leaking pipe

- 13.valve closing
	- In the scenario the robot is using a P controller on each of the arm joint to control how much the joint should move, during experimental results it was shown that controller showed large oscillatory behavior during the initial motion the hand.
		- PD Controller would do a better job at eliminating such error
	- After the controller is changed, the oscillatory behavior disappeared. But now the controller war not eliminating the steady-state error effectively
		- PID controller would do a better job at eliminating the current and previous error

- 14.type of sensor
	- cameras is a Exteroceptive sensor
	- robot need dynamic stability to maintain the balance.
	- Encode sensor can detect the position of its joints through this kind of sensor
	- Tactile sensor can detect touching object
	- ATLAS is not equip with Bump sensor
	- The force torque sensors give internal information of the robot state(Proprioceptive)
	- In some parts of the task, we want ATLAS not to be compliant but to be? Stiff

