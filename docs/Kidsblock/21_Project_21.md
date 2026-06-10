### Project 21: Fire Extinguishing Tank

#### **(1)Description:**

The line-tracking function of the smart tank has been explained in the previous project. And in this project we use the flame sensor to make a fire extinguishing robot. 

When the car encounters flames, the motor of the fan will rotate to blow out the fire. Of course, we need to replace the ultrasonic sensor and two photoresistors with a fan module and flame sensors first.

The specific logic of the smart car is shown in the table below:

| Left Flame Sensors | Right Flame Sensors | Status                                          |
| :----------------: | :-----------------: | :---------------------------------------------- |
|        ≤700        |        ≤700         | Car stops, fan starts rotating to blow out the flame |
|        ≥700        |        ≥700         | Car stops, fan starts rotating to blow out the flame |
|        ≥700        |        ≥700         | Car stops, fan starts rotating to blow out the flame |
|       ＞700        |        ＞700        | Fan stops, car moves                            |

<span style="color: rgb(255, 76, 65);">**Note:**</span>
1）This experiment requires the use of a fire source. Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. 
2）The flame sensoris not fireproof, please do not burn it directly with flame.
We can control an external LED with the flame sensor. The LED still is connected to D9. When fire is connected, LED will be on.


#### **(2)Flow chart:**

![](media/wps120.png)

#### **(3)Connection Diagram:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

<span style="color: rgb(255, 76, 65);">Note:</span>

GND, VCC, SDA and SCL of the 8x16 LED panel are connected to G（GND, V（VCC), A4 and A5.

G, V and A of two flame sensors are interfaced with G（GND), V（VCC), A1 and A2 of the expansion board.

#### **(4)Test Code:**


You can also drag blocks to edit your code, as shown below

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/2e3d4904d9605dfecb5736b4bf235ab2.png)

（4） ![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（5） ![](media/4b40151c7482ff9371570978b8ef9c77.png)

（6）![](media/c0365237fa7ec7de10e9fc465353fae1.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/c07c09e5533a37838722b8c2b513646d.png)

#### **(5)Test Results:**

After upload the test code successfully, power up and turn the DIP switch to ON end. The smart car will put out the fire when it detects flame.

![](media/2de5f1d832d40c0fc94274f1d87443c6.jpeg)

<span style="color: rgb(255, 76, 65);">**Note:**</span>
Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. The flame sensor is not fireproof, please do not burn it directly with flame.
