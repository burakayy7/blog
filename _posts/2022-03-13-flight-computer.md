---
navigation: true
cover: assets/images/plane/plane-computer3.jpg
title: "Plane Project: Designing the Flight Computer"
date: 2022-03-13
class: post-template
tags: plane
layout: post
current: post
subclass: 'post'
---

To fly and eventually control my glider plane, I will need to build some sort of flight controller.

## Design Requirements

When designing this board, there are a few things to think about:

 - Needs to be relatively low-cost and low-power
 - Have at least 6-8 PWM output channels
 - Have a decently powerful processor and memory

Also, at first I tried to implement a 3.3 Volt Arduino, however I reached a few challeneges while trying to integrate a 3.3v microcontroller with a 5v system. So to make things easier for me at first, I decided to also mandate **a 5v based microcontroller**.

This limits us to basically one board: [Arduino Nano Every](https://store.arduino.cc/products/arduino-nano-every?srsltid=AfmBOorussHllcNNi7DAuhcRlTEKWFRgRz5NkDBpnv1aMg8-ZC8_AIm3).




## Wiring

I have drawn up a simple wiring diagram on my _Project Notebook_:
![img]()

For the first version, there will be only two characteristics: read data packets from the radio reciever and send control signals to the control surfaces.

After I have soldered everything by hand, here is the final result:
![img](assets/images/plane/plane-computer2.jpeg)




## The Case
![img](assets/images/plane/plane-computer3.jpeg)