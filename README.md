# robotics-motion-control-subsystem
This project is a custom PCB and firmware for controlling dual-axis stepper motors for a pan-tilt robotics system project for the Robotics and Advanced Tech Society

## System Architecture

### Hardware Overview
The system is built around a custom PCB designed to control dual-axis motion using stepper motors. The board integrates two DRV8825 drivers to independently control two NEMA 17 stepper motors for X–Y positioning.

The PCB accepts a high-current 24V input supply (10A+) and distributes power across the system. It includes support for a buck converter module to step down voltage for lower-power components. Regulated outputs are provided to power an external Raspberry Pi as well as an auxiliary DC motor used elsewhere in the system.

Motor control signals (STEP, DIR, ENABLE) are routed from the microcontroller to each driver. The board also exposes configurable microstepping via MS1–MS3 switches, allowing runtime adjustment of motor resolution. A hardware reset button is connected to the driver reset pins for quick system resets.

### Firmware Overview

The firmware is programmed in C++ using the Arduino IDE. It is responsible for translating high-level positioning commands into precise motor control. Angle inputs are generated externally using OpenCV and passed to the control system.

These angles are converted into step counts based on the stepper motor resolution and microstepping configuration. The firmware continuously updates motor positions in a control loop, issuing step pulses to achieve the desired orientation.

A targetDetected state variable determines system behavior:

Idle / Scan Mode: When no target is detected, the system performs a slow horizontal sweep.
Tracking Mode: When a target is detected, the system adjusts both axes to align with the computed angles.

## General Control Flow
#### Receive target angle input from vision system
v
#### Convert angles to step count
v
#### Compare with current motor position
v
#### Generate step pulses to reduce error
v
#### Repeat in continuous control loop
