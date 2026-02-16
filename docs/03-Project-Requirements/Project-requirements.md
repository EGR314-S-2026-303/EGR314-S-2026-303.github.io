---
title: Project Requirements
---

## Intro

These project requirements are the expectations we will follow while designing and building our device. To create these requirements, we looked at the features from the selected design concept and class requirements; extracted them into tangible goals we can meet with our product. Requirements are split between the Measure of Threshold(MoT), being the minimum level required to not be deemed a failure, and Target Measure, being the goal we want our requirements to reach. Notably, there are many stretch requirements. These requirements are not something we need to include in our device to achieve our base goal. Including these stretch requirements will give our device an edge in the marketplace, if we are able to reach them.

## Requirements

| # | Requirement Description | Measure of Threshold (MoT) | Target Measure | Stretch Requirement (Y/N) |
|---:|---|---|---|:---:|
| 1 | Drone must move over rough/rocky ground | Can consistently drive 5 mph over dirt and gravel. | Can drive 10 mph over dirt and large (5x5x5 in. average) smooth rocks. | Y |
| 2 | Surface mounted, 3.3V switching power regulator | 3.2V | 3.3V | N |
| 3 | Wireless Communication | Bidirectional communication between vehicle and control | Bidirectional communication between vehicle and control or status feed without wires | N |
| 4 | Remotely controlled with WIFI | Controls within 10 meters | Control reach 30 meters or more | N |
| 5 | Stable while moving | MoT of #1 without flipping over | MoT of #2 without flipping over | N |
| 6 | Stable video while moving | Must be able to hold the camera steady while driving at 5 MPH | Must be able to hold the camera steady while driving at 10 MPH | Y |
| 7 | Display live video | Sends out 30 FPS per second | Live video with less than 3 seconds of delay | Y |
| 8 | Microphone | Playback audio from microphone on control device | Able to hear a conversation a meter away from drone | N |
| 9 | Human Design Interface; Respond manually with buttons | Small OLED screen with pushbuttons that permits a user to view all sensor data in text; directly control the actuator; modify setpoints on all the system boards; toggle GPIO debug pins on ALL subsystems. | All the content in MoT and ability to tune sensors and actuators with controls on exterior of device. | N |
| 10 | Use thermal sensors to people with drone | Drone is able to see human heat signatures | Able to see a human body or track residual human body heat 5 meters away | Y |
| 11 | Mechanism that can flip bot over if upside-down | Arm can flip over device, manipulate small rocks (3x3x3 in. max, 1 lb) | Arm can flip over device, manipulate small rocks (3x3x3 in. max, 10 lb) | N |
| 12 | Bot must have decent wireless range | Receives and sends signals from 30 meters away. | Receives and sends signals from 5 km away. | Y |
| 13 | Fast charging | 2 hours charge | 1.5 hours charge | Y |
| 14 | Detect objects with distance sensors | Detects objects within 1 meter of the drone | Detects objects within 3 meters of the drone | N |
| 15 | I2C or SPI | Control peripheral devices such as sensors, microphones, and camera | Same as MoT | N |
| 16 | Daisy chain UART | Daisy chain UART connection between all subsystems | Separate UART loops for high speed communication through certain subsystems | N |
| 17 | Distance controlled wheel speed | The robot can control wheel speed and can display its speed within +-10 cm/s error, and can drive backwards. | MoT and robot uses sensors to determine speed, maneuver around obstacles by turning, and knows speed within +- 1 cm/s error. | Y |
| 18 | Device must be able to communicate to survivors using a speaker | Is able to playback audio sent from an HMI device and listen to its environment. | Is able to playback audio sent from an HMI device and listen to its environment in a hearable range of 90 db, 2 - 5 kHz. | Y |
| 19 | Senses ground vibrations | Can sense ground vibrations (Yes or no) | Can sense ground vibrations that align with footsteps (20-150 Hz) | Y |

## Subsystem and Requirement Designation

| Person | Designated Subsystem | Requirements |
|---|---|---|
| Khalid | Locomotion control | 1, 2, 5, 9, 15, 16, 17 |
| Matthew | Wireless | 2, 3, 4, 7, 9, 12, 15, 16 |
| Armando | Arm system | 2, 5, 9, 11, 15, 16 |
| Manny | Camera/distance sensors | 2, 5, 6, 7, 9, 10, 14, 15, 16, 17 |
| Vedaa | Microphone/speaker | 2, 8, 9, 15, 16, 18, 19 |
| Lia | HMI | 2, 3, 7, 9, 16, 18 |

## Reasons for Requirements

Our device will be a search and rescue bot that will need to be capable of operating in natural disaster zones and urban rescue situations. As a stretch goal, we also intend the device to be capable as a land rover in low atmosphere planets, such as Mars. As a search and rescue robot, it needs to be able to locate survivors by sight, sound, and ground vibrations. 

The robot must traverse decently rough and granulated terrain in order to be a viable rescue bot, thus 1 and 5 require the device to drive and be stable on this type of terrain.

Requirements 2, 3, 4, 9, 15 and 16 are based on the project requirements for this course, due to a certain voltage regulator requirement and communication requirements.

For more remote control capability and robot vision, the robot should have a camera that has to stabilize its feed in order to be useful in its intended environment, thus we came up with requirements 6 and 7.

Since our device will be in rocky environments, it might find itself upside down; requirement 11 solves this issue by allowing the device to right itself autonomously.

Requirements 13, an important part for search and rescue operations,  we want it to quickly recharge the battery in between missions so the drone can resume its activities. Faster charging minimizes time and increases the span of time available to locate and find survivors.

Requirement 10 and 14 allows the robot to find survivors who are lost. 

Requirements 11 and 12 allow the robot to function over a large enough search area to effectively help rescue a survivor.

Requirements 8 and 18 allow the robot to communicate with survivors using a microphone and a speaker. The microphone helps detect calls for help and sends it to the operator. The speaker lets rescuers give instructions and guide them to safety. These features make communication possible during search and rescue missions.

For the robot to reliably navigate its environment and avoid obstacles, the device must be able to control its speed accurately and turn. Thus requirement 17 addresses this.

Requirement 19 allows the robot to detect lower frequency vibrations to detect any movement underneath rubble as well as explosives. 
