# Smart-Unlocking-System-with-Face_Recognition

A novel face recognition algorithm with anti spoofing which is used to handle locks with a wireless camera.

## Installation

### Requirements

#### Software Requirements
  * Python 3.3+
  * Cmake
  * Visual Studio C++
  * Anaconda3
  * Arduino IDE
   ##### Python libraries required
  * Numpy
  * OpenCv-Python
  * Deepface
  * Imutils
  * Dlib
  * Face_recognition
  * Scipy
  * Serial
  
#### Hardware Requirements
  *	Solenoid Locks
  * Bread Board
  * Jumper wires
  * Relay Module
  * FTDI Board
  * EPS32 Cam Module
  *	Power Supply
  *	USB Cable

### Installation Guide:

Install all the above mentioned softwares and libraries through their respective websites which are easily available. 

Hardware connections 

Circuit Diagram for connecting ESP32CAM module to a single lock and relay module 

![unknown](https://circuitdigest.com/sites/default/files/circuitdiagram_mic/Face-Recognition-Door-Lock-Circuit-Diagram.png)

Later you can add multiple relay modules to the esp32 cam according to your need we added a total of 3 modules and 3 locks to the system

The basic connections can be understood by this table below

|ESP32-CAM|FTDI Board|
|---|---|
|5V|VCC|
|GND|GND|
|UOR|TX|
|UOT|RX|

|ESP32-CAM|Relay Module|
|---|---|
|5V|VCC|
|GND|GND|
|IO14|IN|

A bread board can be used to make the connections more understandable.

Open the arduino_Code.ino with Arduino IDE 

##### edit the code according to your usage. 

```arduino
const char* ssid = "Enter Your WIFI SSID";
const char* password = "Enter Your WIFI Password";
```
change the values with your wifi ssid and your wifi password




```arduino
int relay = 15;
int relay2 = 13;
int relay3 = 14;
```

change the values according to your pin connections to your relay module

Connect the laptop and FTDI Board with an USB Cable and upload the code.

Now in arduino for the first time click on serial monitor which is on the top left and press the reset button on the esp32 Camera.

You will get an Ip **address** of where the esp32cam is showing the output save this **ip address**.

### now lets train the data and deploy our system

First add your sample face images in the train folder

Open main.ipynb

Run the first cell to import all the required libraries

to train the face encodings edit the following parts of the code with your own variables and image paths wherever applicable

```python3
uday_image = face_recognition.load_image_file("train/uday.jpg")
uday_face_encoding = face_recognition.face_encodings(uday_image)[0]
known_face_encodings = [
    uday_face_encoding
]
known_face_names = [
    "Udaya Sankar"
]
```

You can add multiple encodings for a single face to have more accuracy.

```python3
url = 'http://<Ip address here>/capture'
```
add the url variable with the ip address u got from the arduino IDE

In the next cell under Show time change the ser.port value with the port name for your ftdi you can find this out by opening arduino IDE and Tools -> port.
```python3
ser = serial.Serial()
ser.port = 'COM3'
```

## Usage

You can now Run the cell Showtime which opens up a window with the esp32 cams live video which is captured wirelessly.

To first pass the anti spoofing layers 
You have to blink your eyes and then smile 
After which your face is automatically recognised and the corresponding lock will open for 5 secs.
After which it loops again and the next person can come and repeat the process to unlock their lock.

If the smile is not detected or a person is not recognized within 15 secs of the previous steps successful pass the programme automatically loops back to the first step.

## Video Demo

Here You can see a small demo of how to run and execute our Project.

https://user-images.githubusercontent.com/84168096/166638744-0bd42a73-471c-4bf7-ba4e-f8fbfad70582.mp4





## Thanks

Many many thanks to all the open source contriubtors who made these amazing softwares and libraries to work with.
