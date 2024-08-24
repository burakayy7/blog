---
navigation: true
cover: assets/images/opencv/opencv_roi.jpeg
title: OpenCV ROI Update
date: 2021-09-18
class: post-template
tags: OpenCV
layout: post
current: post
subclass: 'post'
---

I quick update; I got the ROI (non-grayscaled) to move around the frame.


Here is the code, I highly suggest you run it yourself:

```python
import cv2
print(cv2.__version__)
width=640
height=360
snipW=120
snipH=60

boxCR=int(height/2)
boxCC=int(width/2)

deltaRow=1
deltaColumn=1

cam=cv2.VideoCapture(0,cv2.CAP_DSHOW)
cam.set(cv2.CAP_PROP_FRAME_WIDTH, width)
cam.set(cv2.CAP_PROP_FRAME_HEIGHT,height)
cam.set(cv2.CAP_PROP_FPS, 30)
cam.set(cv2.CAP_PROP_FOURCC,cv2.VideoWriter_fourcc(*'MJPG'))
while True:
    ignore,  frame = cam.read()
    frameROI=frame[int(boxCR-snipH/2):int(boxCR+snipH/2),int(boxCC-snipW/2):int(boxCC+snipW/2)]
    frame=cv2.cvtColor(frame,cv2.COLOR_BGR2GRAY)
    frame=cv2.cvtColor(frame,cv2.COLOR_GRAY2BGR)
    frame[int(boxCR-snipH/2):int(boxCR+snipH/2),int(boxCC-snipW/2):int(boxCC+snipW/2)]=frameROI
    
    if boxCR-snipH/2<=0 or boxCR+snipH/2>=height:
        deltaRow=deltaRow*(-1)
    if boxCC-snipW/2<=0 or boxCC+snipW/2>=width:
        deltaColumn=deltaColumn*(-1)
    

    boxCR=boxCR+deltaRow
    boxCC=boxCC+deltaColumn

    cv2.imshow('my ROI', frameROI)
    cv2.moveWindow('my ROI',width,0)
    cv2.imshow('my WEBcam', frame)
    cv2.moveWindow('my WEBcam',0,0)
    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```


How it works, is by having a x-axis and y-axis counter that will change signs when it hits the edges. 
```python
    if boxCR-snipH/2<=0 or boxCR+snipH/2>=height:
        deltaRow=deltaRow*(-1)
    if boxCC-snipW/2<=0 or boxCC+snipW/2>=width:
        deltaColumn=deltaColumn*(-1)
```

And here is the increment step:
```python 
    boxCR=boxCR+deltaRow
    boxCC=boxCC+deltaColumn
```

Finally, here is how the activate ROI capture works (based off variables):
```python
    frameROI=frame[int(boxCR-snipH/2):int(boxCR+snipH/2),int(boxCC-snipW/2):int(boxCC+snipW/2)]
    frame=cv2.cvtColor(frame,cv2.COLOR_BGR2GRAY)
    frame=cv2.cvtColor(frame,cv2.COLOR_GRAY2BGR)
    frame[int(boxCR-snipH/2):int(boxCR+snipH/2),int(boxCC-snipW/2):int(boxCC+snipW/2)]=frameROI
```
That last part actually puts the ROI back into the original frame; again, Highly reccommend that you run this yourself to see it in action!!

That's it! Thanks!!
