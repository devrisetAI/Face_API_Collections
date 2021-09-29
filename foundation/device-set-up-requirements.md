# Device Set-Up Requirements

### 

### Constraints

There are several constraints set in order to obtain an optimal performance:

* The camera is placed in a hallway with a  minimum length of 3 meters.
* Users are not allowed to wear face attributes other than eyeglasses or a mask.
* If there is a recognition failure when the user is wearing glasses or a mask, the user is expected to take off the glasses or mask in order to provide more features for recognition.
* Users’ face needs to be evenly illuminated.
* Users need to walk at an average walking pace.

### Camera Set-Up

* Image resolution, there is no minimum requirement for image resolution, as long as the face resolution is 125 x 125 pixels. Higher-resolution images require a larger minimum face size. For example, if you have 360p camera resolution, the distance camera to people should be less than 45 cm.
* Place the camera in good lighting not too dark or bright and with no backlight.
* Camera height, between 1.5 m - 1.75 m.
* Frame rate, the recommended frame rate is 30 fps. \(at least 25 fps\) 
* Encoder Bitrate, the recommended encoder bitrate is 3 Mbps.
* Codec, the codec should be h.264.
* Give a marker place approximately less than 3 m from the camera to take pictures.

![Marker Example](../.gitbook/assets/image%20%281%29.png)

### Trigger

Some ideas that can be used to trigger photo submissions to the API:

* Printed QR Code
* RFID
* NFC
* Ultrasonic Module
* Infrared Module
* Face location and minimal size



