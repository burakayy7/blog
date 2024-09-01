---
navigation: true
cover: assets/images/opencv/color1.png
title: OpenCV Color Finder
date: 2021-10-31
class: post-template
tags: OpenCV
layout: post
current: post
subclass: 'post'
---

Welcome back; here I want to quickly show a short script that will output the color at a given pixel. Interesting?

Here is the script I am talking about:
```python
import cv2
import numpy as np
print(cv2.__version__)
evt = 0
xVal = 0
yVal = 0
def mouseClick(event, xPos, yPos, flags, params):
    global evt
    global xVal
    global yVal
    if event == cv2.EVENT_LBUTTONDOWN:
        print(event)
        xVal=xPos
        yVal=yPos
        evt = event
    if event == cv2.EVENT_RBUTTONUP:
        evt = event
        print(event)
width=640
height=360
cam=cv2.VideoCapture(0,cv2.CAP_DSHOW)
cam.set(cv2.CAP_PROP_FRAME_WIDTH, width)
cam.set(cv2.CAP_PROP_FRAME_HEIGHT,height)
cam.set(cv2.CAP_PROP_FPS, 30)
cam.set(cv2.CAP_PROP_FOURCC,cv2.VideoWriter_fourcc(*'MJPG'))
cv2.namedWindow('my WEBcam')
cv2.setMouseCallback('my WEBcam',mouseClick)
while True:
    ignore,  frame = cam.read()
    if evt == 1:
        x = np.zeros([250,250,3],dtype=np.uint8)
        y = cv2.cvtColor(frame,cv2.COLOR_BGR2HSV)
        clr = y[yVal][xVal]
        print(clr)
        x[:,:]=clr
        cv2.putText(x,str(clr),(0,50),cv2.FONT_HERSHEY_COMPLEX,1,(0,0,0),1)
        cv2.imshow('Color Picker',x)
        cv2.moveWindow('Color Picker',width,0)
        evt = 0
    cv2.imshow('my WEBcam', frame)
    cv2.moveWindow('my WEBcam',0,0)
    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```

This is pretty similar to the previous lessons on Mouse Clicks, so I will skip over those sections. Instead, let's look at how we choose the the color.

Once you click on the frame, our function stores the x and y coordinates, and we obtain the pixel color using this code:
```python
clr = y[yVal][xVal]
```

The rest of the code is just displaying that on another window, which should be self explanatory.


I also wanted to show a quick program that will output the full color range, in HSV (Hue, Saturation, and Value):
```python
import cv2
import numpy as np
x = np.zeros([256,720,3],dtype=np.uint8)
for row in range(0,256,1):
    for column in range(0,720,1):
        x[row,column]=(int(column/4),row,255)
x=cv2.cvtColor(x,cv2.COLOR_HSV2BGR)
y = np.zeros([256,720,3],dtype=np.uint8)
for row in range(0,256,1):
    for column in range(0,720,1):
        y[row,column]=(int(column/4),255,row)
y=cv2.cvtColor(y,cv2.COLOR_HSV2BGR)
while True:
    cv2.imshow('my HSV',x)
    cv2.moveWindow('my HSV',0,0)
    cv2.imshow('my HSV 2',y)
    cv2.moveWindow('my HSV 2',0,row+40)
    if cv2.waitKey(1) & 0xff == ord('q'):
        break
cv2.destroyAllWindows()
```
HSV is just another color space, like RGB. For more info, please visit [here](https://programmingdesignsystems.com/color/color-models-and-color-spaces/index.html)
Play around with that if you want.

Thanks, see you next time. 