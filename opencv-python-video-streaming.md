---
title: opencv-python-video-streaming
tags: opencv,python,video,streaming,ai
---

[toc!?direction=lr]

# OpenCV video streaming using Python

## Objective
Capture video by using opencv and python on MacBook

### hh

## Env.
macOS Mojave, python 3.7.3, opencv 4.1

## Setup
``` bash
brew install python
pip3 install opencv-python
```

## Create a python file

> Blockquote

> Blockquote

> Blockquote

vim cap-video-ok.py

``` python
import cv2
cv2.namedWindow("preview")
vc = cv2.VideoCapture(0)

rval, frame = vc.read()

while True:

  if frame is not None:
     cv2.imshow("preview", frame)
  rval, frame = vc.read()

  if cv2.waitKey(1) & 0xFF == ord('q'):
     break
```

## Run

``` bash
python3 cap-video-ok.py
```

And I can see the program opens up a window and shows video by using my MacBook camera
