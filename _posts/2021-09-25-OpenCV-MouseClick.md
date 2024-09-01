---
navigation: true
cover: assets/images/opencv/mouse1.png
title: OpenCV MouseCLick
date: 2021-09-25
class: post-template
tags: OpenCV
layout: post
current: post
subclass: 'post'
---

Hello, in this post I wanted to share how to utilize mouse clicks in OpenCV. We will be writing our own functions to implement this:

```python

import cv2
print(cv2.__version__)
evt=0
def mouseClick(event,xPos,yPos,flags,params):
    global evt
    global pnt
    if event==cv2.EVENT_LBUTTONDOWN:
        print('Mouse Event Was: ',event)
        print('at Position',xPos,yPos)
        pnt=(xPos,yPos)
        evt=event
    if event==cv2.EVENT_LBUTTONUP:
        print('Mouse Event Was: ',event)
        print('at Position',xPos,yPos)
        pnt=(xPos,yPos)
        evt=event
    if event==cv2.EVENT_RBUTTONUP:
        print('Right Button Up: ',event)
        pnt=(xPos,yPos)
        evt=event

width=640
height=320
cam=cv2.VideoCapture(0,cv2.CAP_DSHOW)
cam.set(cv2.CAP_PROP_FRAME_WIDTH, width)
cam.set(cv2.CAP_PROP_FRAME_HEIGHT,height)
cam.set(cv2.CAP_PROP_FPS, 30)
cam.set(cv2.CAP_PROP_FOURCC,cv2.VideoWriter_fourcc(*'MJPG'))
cv2.namedWindow('my WEBcam')
cv2.setMouseCallback('my WEBcam',mouseClick)

while True:
    ignore,  frame = cam.read()
    if evt==1 or evt==4:
        cv2.circle(frame,pnt,25,(255,0,0),2)
    cv2.imshow('my WEBcam', frame)
    cv2.moveWindow('my WEBcam',0,0)
    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```

Here we have made a mouseClick function that utilizes the various functions provided by OpenCV:
```python
event==cv2.EVENT_LBUTTONDOWN
event==cv2.EVENT_LBUTTONUP
event==cv2.EVENT_RBUTTONUP
```

And depending on which of these are activated in the window, our code will do something different, like by putting a circle on the location that we clicked on:
```pytyhon
if evt==1 or evt==4:
    cv2.circle(frame,pnt,25,(255,0,0),2)
```

That's it, I hope you found this useful!!

