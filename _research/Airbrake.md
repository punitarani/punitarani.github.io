---
layout: post
title: Airbrake for Sport Rockets [DRAFT]
permalink: airbrake
author: Punit Arani
date: May 15, 2020
abstract: AgentML is an autonomous LLM-agent system that can analyze datasets, write and execute code, train and evaluate machine learning models, and provide visual insights, enabling users from diverse backgrounds to efficiently build and deploy ML solutions without extensive coding expertise.
category: Demo
---

> High School Research Project for the Team America Rocketry Contest 2020
>
> Team 20-6013: Punit Arani, Aidan Huang and Dylan Nguyen
>
> Mountain Ridge High School - Glendale, Arizona

# Design Analysis of Small and Energy-Efficient Active Airbrake System for Sport Rockets

Sport rockets are often simple model rockets designed with the specific purpose of efficiency with overarching criteria and constraints defining the design.
For the Team America Rocket Contest, students have to design a sport rocket each year that reaches as close to the target height and within the time frame given.

## Introduction

In the development of sport rockets for The American Rocketry Contest (TARC), the most important requirement for the rocket is the apogee that it reaches consistently. While there are numerous ways to approach this problem, one of the most common ways teams approach it is by adding or reducing weight.

An airbrake for a rocket is essentially a variable drag system that increases the drag force caused by the rocket. This increase in drag force should in return reduce the maximum height of the rocket.

## Design

Due to the strict weight and dimensions constraints of the rocket, only around 150 grams can be dedicated to the airbrake and supplemental electronics. The airbrake and electronics need to fit within a 2 inch diameter body tube with a maximum length of 10 inches.

### Hardware

#### Design 1

This initial model was designed to increase the surface area of the rocket, thereby increasing the drag. Its design featured a 3D-printed frame. Using a linear actuator programmed to deploy at certain altitudes, fins would push out of the rocket’s body, effectively increasing its drag and wind resistance whilst in air. While the design did succeed in slowing down the acceleration of the rocket as it ascended, it was inconsistent. Often, we found that the downward force acting on the panels made it difficult for them to open, or problems within the code of the actuator caused a deployment failure.

- Voltage: 6 V
- Current: 550 mA
- Power: 3.3 W
- Dimensions: 55mm x 55mm x 100mm
- Weight: 75g

#### Design 2

With the failure of the first design to consistently overcome downward force, design 2 was formulated. Using a servo motor and gear mechanism as opposed to an actuator, the model utilized “petals” that unfolded outward from the tube. Although the panels had less surface area than the first design, they could more consistently open. In addition to this, this design was much shorter, saving some space within the body tube of the model rocket.

- Voltage: 5 V
- Current: 250 mA
- Power: 1.25 W
- Dimensions: 55mm x 55mm x 50mm
- Weight: 45g

### Electronics

#### Design 1

Energy and data efficient set-up recording data and actively controlling the airbrake at up to 2.5 Hz.
Main use case for this would be for rockets achieving target height relatively closely and needs very little correction with less emphasis on accuracy and precision.

- Main Processor: Arduino Micro
  - ATmega32u4, 16 MHz, 32 KB Flash Memory, 2.5 KB SRAM, 1 KB EEPROM.
- On-board sensors:
  - Accelerometer: ADXL 345
  - Barometer: MPL3115A2
- Interfaces:
  - 1 Futaba J Female Connector
  - 1 SD Card Connector
- Power System:
  - 500 mAh Li-Po @ 3.2v boosted to 5v.
- Weight and Dimensions
  - 75g
  - 132mm x 52mm x 40mm

#### Design 2

Accurate and powerful set-up recording data and actively controlling the airbrake at around 50 Hz.
Main use case for this would be for rockets requiring significant altitude correction with high emphasis on the accuracy and precision of the target apogee.

- Main Processor: Arduino Pro Mini
  - ATmega 328, 16 MHz, 32 KB Flash Memory, 2 KB SRAM, 1 KB EEPROM.
- On-board sensors:
  - Accelerometer: ADXL 345
  - Barometer: BMP 388
- Interfaces:
  - 1 futaba J female connector
  - 1 SD card connector
  - 3 switches
- Power System:
  - 1200 mAh Li-Po @ 3.2v boosted to 5v.
- Weight and Dimensions:
  - 68g
  - 95mm x 52mm x 40mm

### Software

## Testing

### Flight #8

One of our first logged flights. Main purpose was to test the functionality of the airbrake and electronics.

- Motor: Aerotech F42-4T
- Target Apogee: 243.84m
- Actual Apogee: 223.81m
- Predicted Apogee: 223.72m
- Actual Deviation: +11.03m or 8.21%
- Prediction Deviation: +0.09m or 0.04%

125 usable data points @ 2.5 Hz.
Although altitude prediction was done post-flight, the prediction algorithm worked extremely well to an accuracy of well under one percent.
However, the actual height graph was very smooth and had no point of inflection marking the deployment of the airbrake, raising suspicion on the functioning of the airbrake.
Over the next few weeks we worked to design a faster computer along with implementing ways to ensure the airbrake actually deployed and was noticeable visually in our graphs.

### Flight #15

One of our first flights with new and improved airbrake fins and improved electronics featuring the BMP 388 barometer.
Main purpose was to reach the target altitude while recognizing airbrake deployment with a slight emphasis on testing the sustainability of the same rocket body.

- Motor: Aerotech F67-6W
- Actual Apogee: 243.38m
- Predicted Apogee: 253.65m
- Apogee Deviation: +0.46m or 0.20%
- Prediction Deviation: +10.27m or 4.22%
- 850 usable data points @ 25 Hz

This was our first flight that we received confirmation of the airbrake deploying as seen in the graph.
However, the prediction algorithm was really inaccurate and
Regardless, this was our first flight that visually displayed the airbrake in action and can be seen in the height graph with a noticeable jump in altitude.
While the sudden spike in altitude (t=3.2s) surprised us initially, we found that this was caused mechanically. As the airbrake opened, it created a large opening in the airframe causing air outside the rocket to be travelling faster than the inside, reducing the pressure inside the rocket causing the barometer to recognize this change in pressure as an increase in altitude.
This was also when we began to notice data corruption as seen in image to the right.
Upon further inspection, we found that this was caused by low-memory available for caching the datastring by the arduino, which was fixed by reducing datastring size.

### Flight #22

One of our last logged flights.
Main purpose was to get as close to the target altitude and time as possible.

- Motor: Aerotech F67-6W
- Actual Apogee: 255.71m
- Predicted Apogee: 261.21m
- Apogee Deviation: +11.87m or 4.87%
- Prediction Deviation: +5.5m or 2.15%

967 usable Data points @ 25 Hz.
We drilled holes in the sides of the electronics tube for air to reduce Bernoulli's effect causing inconsistencies with the barometer.
Still, we have inconsistencies with the barometer as there is a massive dip in altitude after the airbrake deployed showing how the rocket might have gone down in altitude and back up for almost half-a-second which is inaccurate and impossible.
We found the problem to be caused by this almost ballooning effect caused by the rapid opening and closing of the airbrake causing unnecessary change in pressure inside.
With increased data collection, we got a lot of good data for this flight highlighting the extremely accurate prediction algorithm and the deployment of the airbrake.
We also deployed the airbrake after it reached apogee because we needed to increase the flight time and we decided to achieve it by using it post-apogee for a predefined amount of time.

## Conclusion

The data clearly reveals the accuracy and precision of our Airbrake System and its ability to slow down the rocket travelling at a peak velocity of over 0.5 machs to an altitude with a beyond-satisfactory degree of accuracy. With the adoption of the Arduino Pro Mini and the BMP 388 barometer, the on-board computer was able to actively retrieve altitude and acceleration data, to then derive the velocity and predict the apogee and then deploy the airbrake accordingly. These processes were all hard coded onto the on-board computer and allowed the computer to actively deploy and control the apogee of our rockets.
Due to the project disruptions caused by the Covid-19 pandemic, the project had to be halted towards the end of its final prototype stage resulting in the use of our semi-final algorithm. With further developments and iterations to the code and the hardware design of the airbrake itself, proper field testing is further required to prove the enhanced accuracy of our upgrades.
Regardless, our variable-drag aircraft system proved the ability to not only control a mid-power rocket's altitude, but also the incredible degree of accuracy it conducted its calculations and flights to.
