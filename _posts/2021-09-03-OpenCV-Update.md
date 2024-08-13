---
navigation: true
cover: assets/images/AutoCorr/ma.png
title: OpenCV Update
date: 2021-09-03
class: post-template
---

Hello, 

I just wanted to give a quick update on my progress on learning AI.

I am now able to calculate FPS (frames per second) and put/add text or shapes to the frame window:




```python
import cv2
print(cv2.__version__)
import time
width=640
height=360
myRadius=30
myColor=(0,0,0)
myThick=2
fontH=2
fontT=2
myText='Paul is Boss'
myFont=cv2.FONT_HERSHEY_DUPLEX
upperLeft=(250,140)
lowerRight=(390,220)
lineW=4
cam=cv2.VideoCapture(0,cv2.CAP_DSHOW)
cam.set(cv2.CAP_PROP_FRAME_WIDTH, width)
cam.set(cv2.CAP_PROP_FRAME_HEIGHT,height)
cam.set(cv2.CAP_PROP_FPS, 10)
cam.set(cv2.CAP_PROP_FOURCC,cv2.VideoWriter_fourcc(*'MJPG'))
tLast=time.time()
fpsFLT=10
time.sleep(.1)
while True:
    dT=time.time()-tLast
    fps=1/dT
    fpsFLT=fpsFLT*.9+fps*.1
    print(fps)
    tLast=time.time()
    ignore,  frame = cam.read()
    frame[140:220,250:390]=(255,0,0)
    cv2.rectangle(frame,upperLeft,lowerRight,(0,255,0),lineW)
    cv2.circle(frame,(int(width/2),int(height/2)),myRadius,myColor,myThick)
    cv2.putText(frame,myText,(120,125),myFont,fontH,(0,0,255),fontT)
    cv2.rectangle(frame,(0,0),(120,40),(255,0,255),-1)
    cv2.putText(frame,str(int(fpsFLT))+' fps',(5,30),myFont,1,(0,255,255),2)
    cv2.imshow('my WEBcam', frame)
    cv2.moveWindow('my WEBcam',0,0)
    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```
