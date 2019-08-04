# python-face-detection

## About:
In this tutorial, I will be explaining on face detection application using OpenCV in python3.
If I am to define object detection, it is detecting any object trained upon and finding its exact location on the image or video frame.

Firstly go to your terminal and paste this to clone the repository which contains the code and the pre-trained model for face detection.

` git clone https://github.com/steve7158/python-face-detection.git `
Now follow through the tutorial

Detecting Faces in an ImageFace Detection and Recognition by mariakhalidnaveed ...
## Tutorial:


1. `cd python-face-detection`


2. Download python OpenCV, go to your terminal and type



`sudo python3 -m pip install opencv-python`


3. Move to the cloned directory, open a text editor to work on. Import cv2 for python OpenCV library.


```

import cv2


import sys

```



4. Load the pre-trained data to the memory and initialize a classifier. Finally to get the input data initialize the OpenCV's VideoCapture function and pass the argument 0 to start webcam or video file path if you want test it on a save video file.
```
cascPath = "haarcascade_frontalface_default.xml"

faceCascade = cv2.CascadeClassifier(cascPath)
video_capture = cv2.VideoCapture(0)
```
5.  Initialize a loop, read the video data using the read function, this will return us 2 values namely a boolean value and the frames(images) of the video.



```
while True:


ret, frame = video_capture.read()



convert the color of the frames to grayscale.


gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)


```
Now call in the face detector to analyze the object in the image over multiple scales, this is where we call in open cv's MultiScale function.

`MultiScale: Detects objects of different sizes in the input image. The detected objects are returned as a list of rectangles. (reference: https://www.docs.opencv.org/2.4/modules/objdetect/doc/cascade_classification.html#cascadeclassifier-detectmultiscale )`


### Arguments:

1. the first argument is the image where we are detecting the object on.

2. scaleFactor: Parameter specifying how much the image size is reduced at each image scale.

3. minNeighbors: Parameter specifying how many neighbors each candidate rectangle should have to retain it.

4. minSize: Minimum possible object size. Objects smaller than that are ignored.

5. flags: Parameter with the same meaning for an old cascade as in the function cvHaarDetectObjects. It is not used for a new cascade. 
`faces = faceCascade.detectMultiScale( gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30), flags=cv2.CASCADE_SCALE_IMAGE )`

Now to draw a rectangle, call in the rectangles bottom corner coordinate and the width and height of the rectangle calculated in the above method. By using open cv's rectangle function draw a rectangle.

### Argument:

1st: Image.
2nd: Coordinates of the bottom corner.
3rd:  Coordinates of the top corner.
4th:  Color (in RGB pattern).
5th:  Thickness.
```
for (x, y, w, h) in faces:

cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
Get the output video.
cv2.imshow('Video', frame)
```

Tell the program when to break the loop (i.e. Here by pressing 'q')


```
if cv2.waitKey(1) & 0xFF == ord('q'):

break

```
