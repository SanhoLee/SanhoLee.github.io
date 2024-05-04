---
layout: post
title:  "Finger Controller with Servo Motor."
date:   2024-04-09 11:50:33 +0900
categories: Project CV
tags: [serial, motor]
permalink: /:categories/2
img_path: /imgs/pjt/cv/fingerController/
---

## Preview - How to work
**Please find rotating propeller on image. It works by my fingers**
![preview](preview.gif)
_How it works : Detected? then control the motor_


---

## **Prologue🤔**

After I've learned how to send serial signal to arduino device, I wanted to make its application based on computer vision. but it should simple. 

![serialComm](What-is-Serial-Communication.jpg)
_concept of serial communication_

My idea was combining just like object detection and something could make any values from it.

Yes, nothing very special, but through this project I could understand and remind me of the logic again by making the application. Of course, It was very exciting that I could use computer vision tech in the same time.

## **Development Environment⚙️👨‍💻**

- OS : Windows 11
- IDE : Visual Studio Code
- Languages : python, C(for arduino)
- Refered libraries: 
    1. [cvzone][1], I used it as enabling serial communication with the arduino, however It also has computer vision features on it. 
    2. [mediapipe][2], Take a role for computer vision part.(detecting hand landmarks.)

## **Tasks and Key functions**🛠️**🖼️**

**\[ Processing the tasks \]**

1. Detecting finger landmarks
2. Calculating a distance between first and second finger.
3. Sending the distance value to arduino.
4. Controlling Servo motor communicating with the arduino based on the distance value.


**\[ Key functions \]**

### **1. Detecting Finger Landmarks and Calculating the distance**
- Refered `Hand landmark detection` of `MediaPipe`, You can also refer to this [page][3] and [code][4].
- It can detect each point of hand landmarks so that coordiante information of landmarks could be gained by the index.
- So I just picked the data of `4.THUMP_TIM` and `8.INDEX_FINGER_TIP` to calculate its distance. 
- The value could be increased and decreased when I enlarge and narrow down two fingers, just like zoooming in and out the photos on my iphone.
![hand Landmark by mediapipe](hand-Landmark-mediapipe.png)
_Index of hand landmark by mediapipe_
**Anyway, now  I could use this value to control servo motor integrated in a breadboard. easy.**


### **2. Sending the distance value to arduino by serial communication protocol.**
- This is kind of the protocol, you can refer this [article][5].
- Even though I used encapsulated library `cvzone`, I could find the origin and the process to handle serial communication.

**arduino code on the deivce**
- `SerialData` defined in `ino` file, has `Get` method. 
```c
#include <cvzone.h>
SerialData serialData(1, 3); //(numOfValsRec,digitsPerValRec)
...
void setup() {
    ...
    serialData.begin();
    ...
}
...
void loop() {
    ...
    serialData.Get(valsRec);
    ...
}
```
- I could assume that it is related with commonly used library `Serial` in arduino. 
![arduino serial read](arduino-serial-Read.png)
_read method of `Serial`_

**python code in host device**
- `senddata` one of methods from `cvzone` is actually refering `write` method of `pyserial`.

```python

from cvzone.SerialModule import SerialObject
arduino = SerialObject()
...
def send_int_toArduino(self, dist):
    arduino.sendData([dist])
...

```

![pyserial write method](pyserial-write-method.png)
_write method of `pyserial`_


### **3. Integrating Servo motor and make it move with the distance value.**

The board looks like this..
![bread board setup](bread-board-setup.jpg)
_bread board setup_

- By using `Servo` libary, servo motor can communicatig with arduino and rotating the wheel.
- In the codes, I attached it to a specific pin of arduino, And wrote the distance depend on my finger movement.
- What I found about adjustable angle range, It ranges from 0 to 179 degree.(correct me if i'm wrong 😅)

```c
#include <Servo.h>
Servo myServo;

void setup() {
  myServo.attach(servoOutPin);
...
}

void loop() {
    ...
myServo.write(dist_servo);
    ...
}
```

---

## _**[Details of the code(Github) ⚙️][6]**_

**Let's keep make tiny projects. See ya.🤖**

<!-- should be set with corresponding number on the article. -->

[1]: https://www.computervision.zone/
[2]: https://developers.google.com/mediapipe/solutions/vision/hand_landmarker
[3]: https://developers.google.com/mediapipe/solutions/vision/hand_landmarker/python
[4]: https://colab.research.google.com/github/googlesamples/mediapipe/blob/main/examples/hand_landmarker/python/hand_landmarker.ipynb#scrollTo=_JVO3rvPD4RN&line=11&uniqifier=1
[5]: https://sanholee.github.io/2024/02/embedded-howToSend-digitalValueToArduino
[6]: https://github.com/SanhoLee/cv_fingerController 