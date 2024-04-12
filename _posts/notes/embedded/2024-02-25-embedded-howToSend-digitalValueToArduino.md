---
layout: post
title: "How to send Digital Value To Arduino"
date: 2024-02-25 12:00:10 +0900
categories: [notes, embedded]
tags: [howToX, arduino]
permalink: /:year/:month/:title
img_path: /imgs/ebd/202402/
---

## **About**
It is about how to send digital values to arduino. I was searching the way how to utilize arduino uno as a example of computer vision. And I could find several examples, such like face tracker and lane follower with wheels and etc. 

Among many of those, I thought `cvzone` library and its use-case example was useful to practice computer vision handling, there is even a youtube tutorial. So, I tryied to follow how to implement and how to use it. 

In that tutorial, I could learn and know the way of how computer vision technique could be used. but computer-vision logic was just operatable in separate normal PC not in arduino uno, because of lack of resources and absence of operation system on it probably. So the idea was just transimit relevant digital signals to arduino  when a specific event happens which is triggered by computer vision processing.

For exampls, if the human face is detectted on camera image, I can make a logic to send positive signal(1) to arudino and it recieves the signal and use it to light up a LED lamp accourdingly. This is all the idea and concept that arduino can do.

## **Concept Diagram**
![concept of data exchange](data_exchange.png)
_concept of data exchange between Processing PC and the arduiono._


## **Computer Vision Processing and Sending the signal from external PC**

```python
import cv2
from cvzone.FaceDetectionModule import FaceDetector
from cvzone.SerialModule import SerialObject

arduino = SerialObject('COM3')

cap = cv2.VideoCapture(0)
detector = FaceDetector()

while True:
    success, img = cap.read()
    img, bboxs = detector.findFaces(img)

    if bboxs:
        arduino.sendData([1,0])
    else:
        arduino.sendData([0,1])
    
    cv2.imshow("Image", img)
    kVal = cv2.waitKey(1)

    if kVal==27:
        break

```
**FaceDetector**
- `FaceDetector` use light weight model of `mediapipe` to detect real time face object.
-  Capsulated in `FaceDetectionModule.py` file

**SerialObject**
- Basically it works by `serial` module, and it can be install by enterng [`pip install pyserial`](https://pyserial.readthedocs.io/en/latest/index.html).
- 2 methods are provided, 
  - `sendData(self, data)` to the serial device.
  - `getData(data)` from the serial device.


## **Recieving digital signal as input from Arduino.**

```c
// ino file
#include <cvzone.h>

SerialData serialData(2, 1); //(numOfValsRec,digitsPerValRec)
int valsRec[2]; // array of int with size numOfValsRec 

void setup() {
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
  serialData.begin();
}

void loop() {

  serialData.Get(valsRec);
  Serial.print("1st :  ");
  Serial.println(valsRec[0]);
  Serial.print("2nd :  ");
  Serial.println(valsRec[1]);

  digitalWrite(13, valsRec[0]);
  digitalWrite(12, valsRec[1]);
  
  delay(300);
}
```
**SerialData**
- It also has 2 methods to communicate with external PC
    - `void Send(int sendVals[])` : send the data to external PC
    - `void Get(int* valsRec)` : get the data from the PC

I've got noticed that there are each paired methods between the device and the PC, to enable serial communication.

## **Working like this 🚀**

>Once a face is detected, It turns green LED on. Else, Red LED on.
{: .prompt-tip }

![faceDetect with arduino](0225_faceDetect_withARD.gif)


## **Reference**
[Computer Vision With Arduino | 2 Hour Course | OpenCV Python](https://youtu.be/mfiRJ1qgToc?si=7wzN8Gc_ffSY-miZ)