---
layout: post
current: post
navigation: true
title: "I want to learn OpenCV and AI"
date: 2021-08-03
cover: 'assets/images/opencv/opencv1.png'
class: post-template
---

I have taken a crash course in Python, and I have now found an interest in Artificial Intelligence. And this is how I am going to start.



I am learning this OpenCV and AI topic from [Paul McWhorter](https://www.youtube.com/watch?v=gD_HWj_hvbo&list=PLGs0VKk2DiYyXlbJVaE8y1qr24YldYNDm), he is an amazing teacher!

Today, I would like to share my first AI Python Script. It isn't much, but I am proud of it. But before I show the script, here are the steps for installing OpenCV (I am running these in a [Virtual Enviornment](https://www.youtube.com/watch?v=XCvsLMk4OHM&list=PLGs0VKk2DiYyXlbJVaE8y1qr24YldYNDm&index=4), per Mr. McWhorter's instructions):

```bash
pip install opencv-python=4.5.3.56
```

I am also running all of this in [Visual Studio Code](https://www.youtube.com/watch?v=jyW7zUlvz3o&list=PLGs0VKk2DiYyXlbJVaE8y1qr24YldYNDm&index=4).


```python
import cv2
print(cv2.__version__)
cam=cv2.VideoCapture(1, cv2.CAP_DSHOW)
ret,  frame = cam.read()
print(ret)
cam.set(3,320)
cam.set(4,240)
while True:
    ignore,  frame = cam.read()
    grayFrame=cv2.cvtColor(frame,cv2.COLOR_BGR2GRAY)

    cv2.imshow('my Cam TopRight',frame)
    cv2.imshow('my Cam TopLeft',grayFrame)
    cv2.imshow('my Cam BottomRight',grayFrame)
    cv2.imshow('my Cam BottomLeft',frame)

    cv2.moveWindow('my Cam TopRight',1210,0)
    cv2.moveWindow('my Cam TopLeft',0,0)
    cv2.moveWindow('my Cam BottomRight',1210,552)
    cv2.moveWindow('my Cam BottomLeft',0,552)

    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```

Here is how the code works:
We first import cv2 and make a camera object (called cam) where the video capture will happen. 
the 
```python
cam.read()
```
function will read from the camera, and return a frame. So, to make this a "video", we just repeadetly retrieve frames from the camera. 

And this part of the code will simply just make and move a window to show the frame:
```python
cv2.imshow('my Cam TopRight',frame)
    cv2.imshow('my Cam TopLeft',grayFrame)
    cv2.imshow('my Cam BottomRight',grayFrame)
    cv2.imshow('my Cam BottomLeft',frame)

    cv2.moveWindow('my Cam TopRight',1210,0)
    cv2.moveWindow('my Cam TopLeft',0,0)
    cv2.moveWindow('my Cam BottomRight',1210,552)
    cv2.moveWindow('my Cam BottomLeft',0,552)
```

Finally, we exit this loop if the 'q' key on the keyboard is pressed:
``python 
    if cv2.waitKey(1) & 0xff ==ord('q'):
        break
cam.release()
```

That's it!!

Hope you enjoyed!!
