### Project 10: Light-following Tank


#### **(1)Description:**

In previous projects, we introduced in detail the use of various sensors, modules, and expansion boards on the smart car. Now let’s move to the projects of the smart car . The light-following smart cars, as the name suggests, is a smart car that can follow the light.

We can combine the knowledge from projects photoresistor and motor drive to make a light-seeking smart car. In the project, we use two photoresistor modules to detect the light intensity on the left and right sides of the smart car, read the corresponding analog values, and then control the rotation of the two motors based on these two data so as,to control the movements of the smart car.

The specific logic of the light-following smart car is shown as below.

![image-20230525113331422](media/image-20230525113331422.png)

#### **(2)Flow chart:**

![](media/wps117.png)

#### **(3)Connection Diagram:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Note: </span>The pin "G", "V" and S of the left photoresistor module are connected to G (GND), V (VCC), A1 respectively;

The pin "G", "V" and S of the right photoresistor module are connected to the G (GND), V (VCC), and A2 respectively.

The 4pin cable is marked with A, A1, B1 and B. The right rear motor is connected to B port of the 8833 motor driver expansion board and the left front motor is connected to A port of the 8833 motor driver expansion board.

#### **(4)Test Code:**


You can also drag blocks to edit your code, as shown below.

（1）![](media/9352e6447f9648efddc7d5a748618332.png)

（2）![](media/1d99d71f5fe52dd2145cb11d75cabb21.png)

（3）![](media/5004e509325dffb32c05afe25abedfc9.png)

（4）![](media/6c6f0492f657c4c78a0497bb86519561.png)

（5）![](media/b8fc70fa8b3f335dcdf0c8ad9ed998c6.png)

（6）![](media/9eb0e93fbd43aa24f2ce656191f7cd79.png)

(7) ![](media/9f023e6f571e597e661a8d71a7f803cb.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">Note:</span> The threshold 650 in the code can be adjusted appropriately according to the specific light intensity.

Do not connect the Bluetooth module before uploading the code, because the uploading of the code also uses serial communication, and there may be conflicts with the serial communication of the Bluetooth, which can cause the uploading of the code to fail.)

![](media/6300174b85f63c05dbdcb3b77188f9dc.png)


#### **(5)Test Results:**

After uploading the test code successfully, wire up, turn DIP switch to the ON end and power on, the smart car follows the light to move.

![](./media/img-20240117093758.png)
