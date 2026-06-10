### Project 1: LED Blinks

#### (1)Description：

![](./media/image-20250709122631704.png)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

For starters and enthusiasts, LED Blink is a fundamental program. LED, the abbreviation of light emitting diodes, consists of Ga, As, P, N chemical compounds and so on. The LED can flash in diverse colors by altering the delay time in the test code. When in control, power on GND and VCC. The LED will be on if the S end is at a high level; otherwise, it will go off.

#### **(2)Parameters:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Control interface: digital port
- Working voltage: DC 3.3-5V
- Pin spacing: 2.54mm
- LED display color: yellow

#### (3)Components Required:

![](./media/image-20250709122437613.png)

#### **(4)8833 Motor Driver Expansion Board:**

The Keyestudio 8833 motor driver expansion board is compatible with the Arduino UNO development board. Just stack it onto the development board when using it.

![](media/d8696e83ade31f2b7c56cc5911eacbd7.GIF)

#### **(5)Connection Diagram:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](./media/image-20250709122655936.png)

<span style="color: rgb(255, 76, 65);">**NOTE:**</span> The LED is connected to the D9 port. Remember to install jumper caps onto the shield.

#### **(6)Test Code:**

You can also drag blocks to edit your code, as shown below.

![](media/cc43ba357acb68a4961adb7e5041b6fe.png)

![](media/26b69cd46ad24e1c900c4fb316430353.png)

![](media/21dc3c24da4271aa7ec2bfdac732eeb3.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/ba4723bab640078eccbe1811da138bc3.png)

#### **(7)Test Results:**

Upload the program, LED blinks at the interval of 1s.

#### **(8)Extension Practice:**

We have known how to control the LED, then let's change the frequency of the LED.

We can the frequency of the LED without changing the pin of the LED. Let's modify the code.

You can also drag blocks to edit your code, as shown below.

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/58c76be4c719a885afb500e8f3b80b85.png)

The test result shows that the LED flashes faster. Therefore, we can draw a conclusion that pins and time delaying affect flash frequency.
