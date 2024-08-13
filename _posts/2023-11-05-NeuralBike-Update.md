---
navigation: true
cover: 'assets/images/mainUnit1.jpg'
title: NeuralBike Update
date: 2023-11-05
class: post-template
---

Today I finally found the time to finish the pcb of the main controller for the Crash detection project. I have been working on this in the background for the past few weeks and it's finally complete today! 

The design is somewhat simple. On the top there's the Particle Boron LTE (which will be running inference) and there's also the MPU6050 (the IMU used to collect acceleromter data). But we also need to store that data so on the bottom there's a SD Card Module. This module runs on 5 volts but the Particle Boron runs on 3.3 volts, so to make them compatible, I shorted the input and the output of the voltage converter on the module so that it can run on 3.3 volts. 

On the Boron, the 12c Pins for the MPU6050 has its own dedicated pins (unlike Arduino related microcontrollers). Also, for the SPI pins for the SD card module, the Boron also has it's own MISO/MOSI (D11/D12 respectively) plus its own SCK pin (D13). Now, for the CS pin, the default is A5, so that's what I used.

I just used basic wires to solder them together and voila! I also had to add a piece of perfboard to the SD Card Module because it was getting really hard to get a strong joint.

Here is a picture if you want to see how the final product turned out:

![The main pcb](assets/images/mainUnit2.jpg)

Now I need a good case to put this in. I finally ended up with this design:

[You can view the deisgn in Onshape(the tool I used to design it)](https://cad.onshape.com/documents/1df18ac347a74cac98dfa207/w/4d75f3240e6fd7c24029e563/e/14ce5f3b6cddb572a7779c39?renderMode=0&uiState=654a8f6bdce69c30eab54bf9)

I will  post further updates on the code for this!!
