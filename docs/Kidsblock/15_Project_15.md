### Project 15: IR Remote Control Tank

![](./media/image-20250709134800790.png)

#### **(1)Description:**

Infrared remote control is one of the most common remote control applications found in electric motors, electric fans, and many other household appliances. In this project, we use the knowledge we learned before to make an infrared remote control smart car.

In the 9th lesson, we tested the corresponding key value of each key of the infrared remote control. In this project, we can set the code (key value) to make the corresponding button control the movements of the smart car, and display the movement patterns on the 8X16 LED dot matrix.

The specific logic of the smart car is shown in the table below:

|                 Ultrasonic key                  | Key value | Instructions from keys                                       |
| :---------------------------------------------: | :-------: | ------------------------------------------------------------ |
| ![](media/b11dc5ffa6cccebc6088e5d557d76daf.png) |  FF629D   | Move forward（set PWM to 200）<br />display the pattern of going forward |
| ![](media/ae8110034aacb083151cfd882ee599ba.png) |  FFA857   | Go back（set PWM to 200）<br />display the pattern of going back |
| ![](media/bce9cba2c6d2465fbcce570ad4210eba.png) |  FF22DD   | Turn left<br />display the pattern“STOP”                     |
| ![](media/ad907a618af86f30d52986bbbd57ba76.png) |  FFC23D   | Turn right<br />display the pattern of turning left          |
| ![](media/9716a4ed61a4064d2f47a7b73eccaf87.png) |  FF02FD   | Stop<br />display the pattern“STOP”                          |

**Initial setting: 8X16 LED dot matrix shows the pattern“![](media/dc59c5fcb4fcf6af4d4a5ebb14b7a919.png)”**



#### **(2)Flow chart:**

![](media/wps121.png)

#### **(3)Connection Diagram:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Note:</span>

GND, VCC, SDA and SCL of the 8x16 LED panel are connected to G（GND), V（VCC). A4 and A5 of the expansion board.

Since the 8833 board integrates the IR receiver, you don’t need to wire it up. The pins of the IR receiver are G（GND), V（VCC) and D3.

#### **(4)Test Code:**

You can edit blocks to build up your code

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/a9042e77ebe3009fbb7653bef3429b66.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6）![](media/51e30aa2aca3a7da67ee4f0f81c7dad1.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/7ab62148fa2a23259b8039475978d8fc.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/fae6c22640ced038daca9cb6721ab95e.png)

#### **(5)Test Results:**

After upload the test code successfully and power up, the smart car can be controlled to move by IR remote control and the 8\*16 shows the corresponding patterns of its movements.

![](./media/img-20240117094223.png)
