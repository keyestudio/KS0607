### Project 7: IR Reception

#### **(1)Description:**

![](./media/image-20250709133757050.png)

There is no doubt that infrared remote control is ubiquitous in daily life. It is used to control various household appliances, such as TVs, stereos, video recorders and satellite signal receivers. Infrared remote control is composed of infrared transmitting and infrared receiving systems, that is, an infrared remote control and infrared receiving module and a single-chip microcomputer capable of decoding.   

The 38K infrared carrier signal emitted by the remote controller is encoded by the encoding chip in the remote controller. It is composed of a section of pilot code, user code, user inverse code, data code, and data inverse code. The time interval of the pulse is used to distinguish whether it is a 0 or 1 signal, and the encoding is made up of these 0 and 1 signals. 

The user code of the same remote control is unchanged while the data code can distinguish the key.

When the remote control button is pressed, the remote control sends out an infrared carrier signal. When the IR receiver receives the signal, the program will decode the carrier signal and determines which key is pressed. The MCU decodes the received 01 signal, thereby judging what key is pressed by the remote control.

![](media/5ad0f889b39646ecb13664511479efc8.png)

Infrared receiver we use is an infrared receiver module. Mainly composed of an infrared receiver head, which is a device that integrates reception, amplification, and demodulation. Its internal IC has completed demodulation, and can achieve from infrared reception to output and be compatible with TTL signals. Additionally, it is suitable for infrared remote control and infrared data transmission. The infrared receiving module made by the receiver has only three pins, signal line, VCC and GND. It is very convenient to communicate with Arduino and other microcontrollers.

#### **(2)Parameters:**

- Operating Voltage: 3.3-5V（DC）
- Interface: 3PIN
- Output Signal: Digital signal
- Receiving Angle: 90 degrees
- Frequency: 38khz
- Receiving Distance: 10m

Infrared receiver integrated on motor drive board：

![](./media/image-20250709133832650.png)

<span style="color: rgb(255, 76, 65);">**Note:**</span> Since the IR receiver is integrated into the Keyestudio 8833 motor drive expansion board, no additional wiring is required. The pins of the IR receiver on the Keyestudio 8833 motor drive expansion board are G (GND), V (VCC), and D3.

#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below

![](media/cfe0841bcc9404c29519ed623195ca6a.png)

![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

![](media/5a48421831518ea8e0c00be83cf4edf4.png)

![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/90978855cddd94c161f9ed02f85b0674.png)

#### **(5)Test Results:**

Upload the code to the development board, and set the baud rate to 9600. Take out the remote control, aim it at the infrared receiving sensor, and press a button to send the signal. You will see the corresponding key value. If the key is pressed for too long, a garbled "FFFFFFFF" may easily appear.

![](media/5c01c594a5a11511cf52466eb5f27e45.png)

Below we have listed out each key value of keyestudio remote control. So you can keep it for reference.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

#### **(6)Extension Practice:**

We have just decoded the key values of the IR remote. Now let's use it to control an LED light on and off. We need to connect an LED light module to the D9 pin, while the pin position of the infrared receiver remains unchanged. When the OK button on the remote control is pressed, the LED connected to D9 will light up, and when the OK button is pressed again, the LED will turn off.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)


You can also drag blocks to edit your code, as shown below

（1）![](media/cfe0841bcc9404c29519ed623195ca6a.png)

（2）![](media/e9da5ac1d1d68eaec6db176ee61326ee.png)

（3）![](media/ba67c48d67b1c9753fca82964c9dddc7.png)

(4) ![](media/0aa28f86f26d94bdb4c951c994aa854f.png)

（5）![](media/f8b75df8ccea3efe1cd3ea383b0f88f2.png)

（6）![](media/7406d60c93cdba0b13ded27cba718ec7.png)

（7）![](media/d7be3fa06a1456d46472fffd61823c73.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/57149c79243ff22aa00ff2c54dd4f70b.png)

Upload the code to the development board, and press the “OK” key on the remote control to turn the LED on and off.

![](./media/img-20240117092532.png)
