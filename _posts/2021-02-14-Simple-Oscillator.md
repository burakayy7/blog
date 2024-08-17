---
layout: post
current: post
navigation: true
title: "Simple Oscillator"
date: 2021-02-14
cover: 'assets/images/oscilpic.jpg'
class: post-template
---


For almost the past 2 years, I have been trying to make a simple oscillator circuit without using a 555 Timer. I have tried various ideas with capacitors and transistor but I was never able to figure out how to make them oscillate. Then one day I stumbled upon and idea I found on the internet and that led me to this circuit:
![Simple Oscillator Circuit](assets/images/oscillatorCircuit.jpg)

It might look complicated, but it actually isn't. This type of oscillator is called a CC Relaxation Circuit. It consists of 2 transistors that are paired with 2 capacitors and 2 resistors (there are actually 2 more resistors, but those are for the LEDs). 


It works by alternatingly charging 2 capacitors, through their resistors, to a certain threshold voltage of the transistor \(in this case I am using a BC547 transistor\). For example, let's assume that after the power is plugged in, the left capacitor starts to charge. Once it hits the threshold voltage of the right transistor \(~0.3v\), the transistor turns on and discharges it while also then charging the right capacitor. Once the right capacitor is charged to the threshold, it turns on the left transistor where the cycle repreats. 

The LEDs are there to show that there in deed is an oscillation going on. 

Here is a short video of it in actions:
[video!](https://www.youtube.com/shorts/wjwK-lxBhHE)

Please let me know if have any ideas on how I could explain this better!


