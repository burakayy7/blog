---
navigation: true
cover: assets/images/neuro_drone_1.jpg
title: "Novel Gesture Controlled Autonomous Drone | Part 1: Flight Computer"
date: 2025-02-20
class: post-template
tags: miscellaneous
layout: post
current: post
subclass: 'post'
---

One idea that I've had is to create my own mini autonomous drone, but controlled using a novel gesture-based control system, using a separate pair of gloves. 

In this post, I will be introducing the concept, and starting by showing my progress on the flight computer. 


## The Concept

The idea is to control the drone using hand gestures. The current place is to have a "smart glove" be worn by the pilot, where it will be able to detect if the fingers have made contact with each other, and its orientation. It will combine these various inputs into a control signal which will fly the drone. 

This is the preliminary work-in-progress idea, and is subject to change. 

## Flight Computer Progress

So, since I don't have motor drivers, I decided to use the ones I had theorized in a post a while back: [My Cheap & Simple Optocoupler based DC Motor Driver for 3.3v Devices](https://burakayy.com/blog/opto-motor-driver).

The current flight hardware includes four of these drivers and an MCU. The current roadblock is that due to the minimal space to solder, there's multiple points that contact, when they shouldn't be. This issue is hard to fix as there's little room to operate in. I might need to restart the entire flight computer design. 

![back1](assets/images/drone/IMG_1559.jpeg)


I will be back soon to give updates.