---
layout: default
title: UnityMotorCommand
parent: Arduino
nav_order: 1
---

# UnityMotorCommand
Arduino script that reads serial output from Unity to control the two stepper motors.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Serial commands
The Arduino and Unity communicate with one another over a serial communication port. The serial command is a string sent from Unity to the Arduino and terminating in a new-line character `\n`. Items in the string are separated by spaces. The first item in the string is the method the command is intended to activate (correspondance between methods and command words is established in the Arduino code. The commands and method names match, for simplicity). Any other items in the string are taken as arguments for the method being called.

### Ping
Pings the Arduino (used for testing connection). Responds with "PONG" if the Arduino sucessfully receives the command and if Unity is set up to read serial output from the Arduino (currently not the case because of lag issues and because the experiment isn't currently set up to require information from the Arduino).

### M1F / M2F
Rotates the corresponding motor (1 or 2) forward (clockwise) one step.

### M1B / M2B
Rotates the corresponding motor (1 or 2) backward (counterclockwise) one step.

### M1R / M2R
Whenever one of the motors takes a step, the Arduino continues to send current through the motor to hold it in place. This command releases the motor. 

### moveStepper
Allows Unity to tell the Arduino to move one of the stepper motors a specific amount. The first argument specifies which motor, and the second argument corresponds to the number of steps to move (positive is forward, negative is backward).

Example:
```c#
arduino.WriteToArduino("moveStepper M1 -20\n");
```
