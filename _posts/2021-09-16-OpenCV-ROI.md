---
navigation: true
cover: https://github-production-user-asset-6210df.s3.amazonaws.com/120507146/357630125-435d0d8d-14d8-4623-9fc7-5eb3707d3287.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAVCODYLSA53PQK4ZA%2F20240814%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240814T004040Z&X-Amz-Expires=300&X-Amz-Signature=b05e965ba6fb6b757c6d9e396a1bef871162ea628b03b589e40cdf5da0056dc8&X-Amz-SignedHeaders=host&actor_id=120507146&key_id=0&repo_id=841746844
title: OpenCV ROI
date: 2021-09-03
class: post-template
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
