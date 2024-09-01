---
navigation: true
cover: assets/images/opencv/trackbars1.png
title: OpenCV Trackbars
date: 2021-10-22
class: post-template
tags: OpenCV
layout: post
current: post
subclass: 'post'
---

Welcome back, in this lesson I wanted to show you how to use TrackBars in OpenCV.


OpenCV provides functions to use trackbars, the only thing we need to do is to pass a function that is called when the user interacts with the trackbars.

```python
cv2.createTrackbar('xPos','myTrackbars',xPos,1920,myCallBack1)
cv2.createTrackbar('yPos','myTrackbars',yPos,1080,myCallBack2)
cv2.createTrackbar('radius','myTrackbars',myRad,int(height/2),myCallBack3)
cv2.createTrackbar('thick','myTrackbars',myThick,7,myCallBack4)
```

Here are our corresponding four functions:
```python
def myCallBack1(val):
    global xPos
    print('xPos: ',val)
    xPos=val
def myCallBack2(val):
    global yPos
    print('yPos: ',val)
    yPos=val
def myCallBack3(val):
    global myRad
    print('Radius: ',val)
    myRad=val
def myCallBack4(val):
    global myThick
    print('Thickness: ',val)
    myThick=val
```

These will decide what happens when we interact with a trackbar, in this example, we will be moving around a circle in the frame. 


Putting this all together, you get this:

```python
import cv2
print(cv2.__version__)
def myCallBack1(val):
    global xPos
    print('xPos: ',val)
    xPos=val
def myCallBack2(val):
    global yPos
    print('yPos: ',val)
    yPos=val
def myCallBack3(val):
    global myRad
    print('Radius: ',val)
    myRad=val
def myCallBack4(val):
    global myThick
    print('Thickness: ',val)
    myThick=val
myRad=25
width=640
height=360
myThick=1
xPos=int(width/2)
yPos=int(height/2)
cam=cv2.VideoCapture(0,cv2.CAP_DSHOW)
cam.set(cv2.CAP_PROP_FRAME_WIDTH, width)
cam.set(cv2.CAP_PROP_FRAME_HEIGHT,height)
cam.set(cv2.CAP_PROP_FPS, 30)
cam.set(cv2.CAP_PROP_FOURCC,cv2.VideoWriter_fourcc(*'MJPG'))
cv2.namedWindow('myTrackbars')
cv2.resizeWindow('myTrackbars',400,150)
cv2.moveWindow('myTrackbars',width,0)
cv2.createTrackbar('xPos','myTrackbars',xPos,1920,myCallBack1)
cv2.createTrackbar('yPos','myTrackbars',yPos,1080,myCallBack2)
cv2.createTrackbar('radius','myTrackbars',myRad,int(height/2),myCallBack3)
cv2.createTrackbar('thick','myTrackbars',myThick,7,myCallBack4)
while True:
    ignore,  frame = cam.read()
    if myThick == 0:
        myThick=(-1)
    cv2.circle(frame,(xPos,yPos),myRad,(255,0,0),myThick)
    cv2.imshow('my WEBcam', frame)
    cv2.moveWindow('my WEBcam',0,0)

    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```

I hope you enjoy this super short lessons on OpenCV! Soon we will get into more complicated projects!!

See you next time!