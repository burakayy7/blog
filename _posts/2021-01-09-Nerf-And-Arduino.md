---
navigation: true
cover: ""
title: Nerf And Arduino
date: 2021-01-09
class: post-template
layout: post
current: post
subclass: 'post'
tags: 
---

Hello, I wanted to share with you a small project I did. It involves a wearable, Arduino Powered, Nerf Gun!!

See, after watching Iron Man, I really wanted to build my own "arm gun". And I had a old automatic nerf gun lying around, so I got an idea: repurpose the old nerf gun parts, fuse them with Arduino, and design a way to wear it.

## How does an Automatic Nerf Gun Work

If you have every gotten the chance to take a nerf gun apart, you will see two DC motors (at least the ones that are battery powered). And if you ever experimented with it, you will see that the motors actually rotate in opposite directions. So how does this work?

### Motor Launching

Below is a diagram I drew to illistrate this concept:

![img](assets/images/nerfmotor.png)

As you can see, the alternate rotating wheels "propell" the robot forwards.
And the friction that is generated from the motor attachments is what grips the motor.

The only thing that is required is a way to feed each bullet into the wheels.

### The Arm

To handle this task, I carefully investigated how the nerf gun handles this, and it is basically done by utilizing a lever that will "push" each bullet into the motors. But since this has to be completly electronic, I need an alternative solution. This is where Servo motors come in. 

The plan is to use a servo motor to push the "plug" that is utilized in the nerf gun. 

Below is a picture of how the setup looks like:
