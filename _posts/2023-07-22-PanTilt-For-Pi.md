---
navigation: true
title: "Raspberry Pi Cam PanTilt"
date: 2023-07-22
cover: 'assets/images/piCamImg/final.jpg'
class: post-template
layout: post
current: post
subclass: 'post'
---
After wanting to do experiment with AI on my Raspberry Pi 4, I decided to build a Servo actuated Pan-tilt mount from scratch. For the past few days, I have been working hard 3d modeling a mount that not only works but also looks good.

I have a whole seperate github repository for it [here](https://github.com/burakayy7/Servo-PanTilt-PiCam). That is also were you can find the CAD files!!

# Servo-PanTilt-PiCam
I decided to make a Pan-tilt Servo mount for the Raspberry Pi Camera. It is ment for the common 9g servos. I first thought of this to use in Paul McWhorter's Raspberry Pi class, put know maybe I might use it in a few of my own projects as well. I've included all the 3D Models and code. Use this however you like! Enjoy!

First, print out the cad files. 
![image](assets\images\piCam\images\parts.jpg)

Then I got one of my servos, and put it in the quadropod mount where the wires are facing the back \(the front is where the 2 legs point forwards\). I then screwed it in with the 2 long screws servos come with. 
![2](assets\images\piCam\images\images/1.jpg)

Then I programmed the servo to be at 90 degrees because now we put the horn \(the 2 sides one\). I customized this horn \(trimming about 1-2 millimeters from either end and driling a wider hole\) to fit in the horn slot in the servo mount. The slot in the servo mount is too small for this horn. Next, I screwed in the horn with the small screw. 
![3](assets\images\piCam\images\images/horn.jpg)

Then, I screwed in the panMount to the horn of the servo with 2 screws of the right diameter. Make sure to use screwes that have a small base, or else the next servo won't fit in place.
![4](assets\images\piCam\images\images/2.jpg)

After this, it gets a bit complicated. You first need to screw in the tilt mount to it's hole and then orient it in such a way, that you'll have room to put the next servo in. 
![5](assets\images\piCam\images\images/3.jpg)

Then program the 2nd servo to be in 60 degrees and put it's small horn in facing parallel.  
![6](assets\images\piCam\images\images/horn2.jpg)

Next, put the 2nd servo in it's position on the mount, where the wires come out the front. and also put the horn in it's slot on the tilt mount.
![7](assets\images\piCam\images\images/4.jpg)

This is when you screw in the horn for the second servo. However, you have to get a new screw that is the same radius as the given one, but longer. 
![8](assets\images\piCam\images\images/5.jpg)

Then, I screwed in one of the long screws that came with the 2nd servo on the back mount:
![9](assets\images\piCam\images\images/screwHorn.jpg)

I then programmed the servo to be at 180 degrees for me to screw in the other one. 
![0](assets\images\piCam\images\images/6.jpg)

And finally, we screw in the Pi Camera. Now the screw holes are kind of delicate, so make sure to use thin screws and be gentle. 
![11](assets\images\piCam\images\images/final.jpg)

AND DONE!! ENJOY!!!!
