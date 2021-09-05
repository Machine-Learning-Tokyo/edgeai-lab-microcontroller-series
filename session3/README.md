# Audio Based Application using Microphone
Our third session of the EdgeAI Lab with Microcontroller Series is to show how to develop a simple Audio Based application using the Digital Microphone device on Arduino Nano 33 BLE Sense board. 

# What is Digital Microphone
Microphones are components that convert physical sound into digital data. Microphones are commonly used in mobile terminals, speech recognition systems or even gaming and virtual reality input devices.
![image](https://user-images.githubusercontent.com/948498/132099176-57e317a7-fd97-4a57-8e2a-73f0a84a62d4.png)

Here is a simple tutorial to [Create Sound Meter using Microphone on Arduino Nano 33 BLE Sense Board](https://docs.arduino.cc/tutorials/nano-33-ble-sense/microphone_sensor).


# Edge AI Applications using Microphone
- Detect Audio Events
- Detect Human Voice
- Keyword Detection
- Detect Detect Respiratory Sound

# Snoring Sound Detection
The aim of this project is to detect snoring sound during sleep by simple microphone.

## Background
Snoring is caused by the rattling and vibration of tissues near the airway in the back of the throat. These sounds occur in low frequency range and can be easily detected using simple models. 

## Blocks of EdgeAI Pipeline
Based on this, let us identify different blocks of the generalized EdgeAI Pipeline.
- Data Collection
  - We will use the public [AudioSet](http://research.google.com/audioset/) dataset for training a 1D CNN model.

- Digital Signal Processing
  - Anotating the snore frames in raw audio data and data extraction for training.

- On Device Deployment and Inference
  - The code uses multithreading. One thread will sample the audio stream and another frame will perform DSP on the data window. A motor vibrator is connected to display the results. It will vibrate when snoring activity is detected.
  - The results are also send via serial port, so you can check the results using Serial Monitor.

## Steps to reproduce the project
### Install Arduino IDE 1.8.14+ 
Please download the IDE from [Arduino Website](https://www.arduino.cc/en/software). Install any version >= 1.8.14 

Please checkout our first session [EdgeAI Lab with Microcontrollers Session #1: Overview of EdgeAI Applications](https://youtu.be/S9Ejmi_3Vrw?t=2412) if you want to refer to quick video guide.


### Add Arduino Mbed OS Core for Nano 33 BLE Sense
The next step is to install the Libraries related to Arduino Nano 33 BLE Sense board.<br>
There is a simple [QuickStart Guide](https://docs.arduino.cc/hardware/nano-33-ble-sense) to install the necessary packages. You can check if the board can be programmed by trying out Simple LED Blink example.


### Install Libraries using Library manager
#### RingBuf Library
You can install libraries from the Library Manager. You can find that from Arduino Tools menu > Manage Libraries > Library Manager.
![image](https://user-images.githubusercontent.com/948498/132113967-d86c06ff-8262-48f9-b668-9425cfc9b32d.png)


### Include the Edge Impulse Library
Please download the [Prebuild Library](snoring_detection_inferencing.zip). We need to add this to our project.<br>
To add, select Sketch menu > Include Library > Add .ZIP Library ...
If you get no error, then everything is fine.
![image](https://user-images.githubusercontent.com/948498/132113862-d9e25ed2-35f2-4eec-ba16-1f28bb485058.png)


### Programming Arduino
To run the example, open the file inferencing.ino in Arduino. Since its .ino file, it will be automatically opened by Arduino IDE if it was installed successfully. If not, then you can open it through the standard operation (File > Open > [Path to inferencing.ino](inferencing/inferencing.ino)).<br>
Click Verify button. It might take a while for compilation and verification process. You should get the following message on successful completion.
```
Done Compiling

Sketch uses 523696 bytes (53%) of program storage space. Maximum is 983040 bytes.
Global variables use 45856 bytes (17%) of dynamic memory, leaving 216288 bytes for local variables. Maximum is 262144 bytes.
```

After that, click on Upload button to upload the firmware to Arduino Nano board.
```
Sketch uses 523696 bytes (53%) of program storage space. Maximum is 983040 bytes.
Global variables use 45856 bytes (17%) of dynamic memory, leaving 216288 bytes for local variables. Maximum is 262144 bytes.
Device       : nRF52840-QIAA
Version      : Arduino Bootloader (SAM-BA extended) 2.0 [Arduino:IKXYZ]
Address      : 0x0
Pages        : 256
Page Size    : 4096 bytes
Total Size   : 1024KB
Planes       : 1
Lock Regions : 0
Locked       : none
Security     : false
Erase flash

Done in 0.001 seconds
Write 524432 bytes to flash (129 pages)
[==============================] 100% (129/129 pages)
Done in 20.619 seconds
```

### Inference from Arduino
The inference results are sent via Serial Port configured with baud-rate of 115200 bps.<br>
You can open up the Serial Monitor from the Tools menu.




