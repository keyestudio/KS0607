### Project 17: Bluetooth Control Tank

#### **(1)Description:**

We have learned the basic knowledge of Bluetooth in the previous project . In this lesson, we will use Bluetooth to control the smart car. Since it involves Bluetooth, a sending end and a receiving end are needed. In the project, we use the mobile phone as the sender (master), and the smart car connected with the HM-10 Bluetooth module (slave) as the receiver.

We have learned earlier that sending a bit can control LEDs. And the principle of controlling this robot car is the same.

In order to better control the intelligent tank robot, we specially made an APP. In this lesson, we will read all the key value on this APP through code, and then introduce the exclusive APP of our tank robot.

#### **(2)Key Function on the APP:**

The following table illustrates the functions of corresponding keys:

|                      Keys                       |                                                |                          Functions                           |
| :---------------------------------------------: | :--------------------------------------------: | :----------------------------------------------------------: |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) |                                                | Pair and connect HM-10 Bluetooth module;click again to disconnect |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) |                                                |                 select the robot to operate                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) |                                                |       to control the movements of the robot by buttons       |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) |                                                |      To control the movements of the robot by joystick       |
| ![](media/3ab61154b4ae730a3757f40171846825.png) |                                                |       To control the movements of the robot by gravity       |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) |   Send “F”when pressed and “S”when released    | The car moves forward when it is pressed and stops when released |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) |   Send “L”when pressed and “S”when released    | The car turns left when it is pressed tight and stops when released |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) |   Send “R”when pressed and “S”when released    | The car turns right when it is pressed tight and stops when released |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) |   Send “B”when pressed and “S”when released    | The car turns back when it is pressed tight and stops when released |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) |        Send “u”+digit+“\#”when dragged         |          Drag to change the speed of the left motor          |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) |        Send “v”+digit+“\#”when dragged         |         Drag to change the speed of the right motor          |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) |         Select to enter Function page          |                                                              |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Send “G”when pressed and “S”when pressed again | Enter obstacle avoidance mode when pressed and exit when pressed again |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Send “h”when pressed and “S”when pressed again | Enter following mode when pressed and exit when pressed again |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Send “e”when pressed and “S”when pressed again | Enter line-tracking mode when pressed and exit when pressed again |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Send “f”when pressed and “S”when pressed again | Enter move-in-confined-space mode when pressed and exit when pressed again |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Send “i”when pressed and “S”when pressed again | Enter light following mode when pressed and exit when pressed again |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Send “j”when pressed and “S”when pressed again | Enter fire extinguishing mode when pressed and exit when pressed again |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Select to enter facial expression display mode |                                                              |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Send “k”when pressed and “z”when pressed again | Show smiling pattern when clicked and clear expression when clicked again |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Send “l”when pressed and “z”when pressed again | Show disgusting pattern when clicked and clear expression when clicked again |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Send “m”when pressed and “z”when pressed again | Show happy face when clicked and clear expression when clicked again |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Send “n”when pressed and “z”when pressed again | Show sad pattern when clicked and clear expression when clicked again |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Send “o”when pressed and “z”when pressed again | Show disparaging pattern when clicked and clear expression when clicked again |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Send “p”when pressed and “z”when pressed again | Show heart-shaped pattern when clicked and clear expression when clicked again |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) |                                                | Choose to enter the custom function interface; there are six keys 1,2,3,4,5,6; with these keys, you can expand some functions by yourself |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) |               Click to send “w”                | Click to display the analog value detected by the photoresistor on the left |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) |                Click to send“y”                | Click to display the analog value detected by the photoresistor on the right |
| ![](media/a76df707b84409e57a1167889c3510d9.png) |                Click to send“x”                | Click to show the distance detected by ultrasonic sensor (unit: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Click to send“c” <br />Click again to send“d”  |   Press to turn on the fan and press again to turn off it    |

#### **(3)Flow Chart:**

![](./media/image-20250709135203165.png)

#### **(4)Connection Diagram:**

![](media/930a8024364e07505e845624a94c27bd.png)

<span style="color: rgb(255, 76, 65);">Note:</span>

GND, VCC, SDA and SCL of the 8x16 LED panel are connected to G（GND), V（5V), A4 and A5 of the expansion board. STATE and BRK don’t need to be interfaced. The BT module is inserted into the expansion board.

#### **(5)Test Code:**

You can drag blocks to edit your code

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/3b4fb768cbf7e0b80fa55cb15aa932b7.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6) ![](media/8a13abc40d27d0470902e528b40170c3.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/341e0a01bd6a76edb53f9414ef641a75.png)

#### **(6)Test Result:**

After uploading the code, connect the robot to the Bluetooth module and pair the Bluetooth APP. Turn on the powerswitch of the motor drive shield. Place the robot on the floor, you can use these buttons of the Bluetooth app to control the robot. 

![](media/352d5ec83c4246b980da10b5f99711c5.jpeg)

1. The up, down, left and right arrows control the robot to move forward, backward, left and right respectively.

![](./media/img-20240117095015.png)

2. Click the joystick button and pull the direction of the black point in the white circle to control the movement direction of the robot.

![](./media/img-20240117095052.png)

3.Click the Gravity button and tilt the phone in the forward, backward, left, and right directions, and the robot will move in the direction in which the phone istilted.

![](./media/img-20240117095131.png)

