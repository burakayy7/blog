---
navigation: true
cover: assets/images/opencv/opencv_roi.jpeg
title: OpenCV ROI
date: 2021-09-03
class: post-template
tags: opencv
---

Hey, welcome back to another OpenCV update. Today I will be talking about Regions of Interest (or ROIs). Think of it like carving out that piece of chocolate cake that has the good topping! Simply put, it's taking a specific portion of a frame. 

To start, I want to show the full code, so you can follow along with me:
```python
import cv2
print(cv2.__version__)
width=640
height=360
cam=cv2.VideoCapture(0,cv2.CAP_DSHOW)
cam.set(cv2.CAP_PROP_FRAME_WIDTH, width)
cam.set(cv2.CAP_PROP_FRAME_HEIGHT,height)
cam.set(cv2.CAP_PROP_FPS, 30)
cam.set(cv2.CAP_PROP_FOURCC,cv2.VideoWriter_fourcc(*'MJPG'))
while True:
    ignore,  frame = cam.read()
    frameROI=frame[150:210,250:390]
    frameROIGray=cv2.cvtColor(frameROI,cv2.COLOR_BGR2GRAY)
    frameROIBGR=cv2.cvtColor(frameROIGray,cv2.COLOR_GRAY2BGR)
    cv2.imshow('My BGR ROI', frameROIGray)
    cv2.moveWindow('My BGR ROI',650,180)

    frame[0:60,0:140]=frameROI
    cv2.imshow('My Gray ROI', frameROIGray)
    cv2.moveWindow('My Gray ROI',650,90)
    cv2.imshow('My ROI', frameROI)
    cv2.moveWindow('My ROI',650,0)
    cv2.imshow('my WEBcam', frame)
    cv2.moveWindow('my WEBcam',0,0)
    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()

```


So, moving away from the stuff discussed in the previous posts, I just want to show what's new. 

If we treat the frames as a 2D array, 
![](assets/images/opencv/2Darray.png)


then we can easily acces parts or sections of this frame (array) using Python:

```python
frameROI=frame[150:210,250:390]
```
here, we are accessing all pixels from 150 to 210 (on the y-axis) and from 250 to 390 (on the x-axis). 

We can then convert this to a Grayscale image or BGR, respectively, with this function:
```python
    frameROIGray=cv2.cvtColor(frameROI,cv2.COLOR_BGR2GRAY)
    frameROIBGR=cv2.cvtColor(frameROIGray,cv2.COLOR_GRAY2BGR)
```
Finally, with the code here, we make a brand new frame to show in another window:
```python
    frame[0:60,0:140]=frameROI
    cv2.imshow('My Gray ROI', frameROIGray)
    cv2.moveWindow('My Gray ROI',650,90)
    cv2.imshow('My ROI', frameROI)
    cv2.moveWindow('My ROI',650,0)
    cv2.imshow('my WEBcam', frame)
    cv2.moveWindow('my WEBcam',0,0)
    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```

### Question
Can you guess what this line does:
```python
frame[0:60,0:140]=frameROI
```
*hint: replace
