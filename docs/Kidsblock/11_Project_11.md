### Project 11: Ultrasonic Sound-following Tank


#### **(1)Description:**

In the previous lesson, we learned about the light-following smart car. And in this lesson, we can combine the knowledge to make an ultrasonic sound-following car. In the project, we use ultrasonic sensors to detect the distance between the car and the obstacle in front, and then control the rotation of the two motors based on this data so as to control the movements of the smart car.

The specific logic of the ultrasonic sound- following smart car is shown in the table blow:

|                        Detection                        |              Setting              |
| :-----------------------------------------------------: | :-------------------------------: |
| The distance(cm) between the car and the obstacle front | Set the angle of the servo to 90° |
|                      **Condition**                      |           **Movement**            |
|               distance≥20 and distance≤50               |             Go front              |
|            10＜distance＜20<br/>distance＞50            |               Stop                |
|                       distance≤10                       |              go back              |

#### **(2)Flow chart:**

![](media/wps118.png)

#### **(3)Connection Diagram:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

<span style="color: rgb(255, 76, 65);">Note:</span> The wiring of the ultrasonic sensor, the servo and the motor is the same as the previous project experiment. The GND, VCC, SDA, and SCL of the 8x16 LED panel are respectively connected to G (GND), V (VCC), A4, and A5 on the expansion board.

#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below.

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/f6fb93211f786d023eb77eb210eae454.png)

（3）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

(7) ![](media/4b40151c7482ff9371570978b8ef9c77.png)

(8) ![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

(9) ![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

(10) ![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/b895ca60e3249e09d4c15c356c60099a.png)


#### **(5)Test Result:**

Upload the code, power up, and turn the DIP switch to ON. The servo will rotate 90°, the 8X16 LED panel will show ![](media/fdd4ae50b3372cc9c4ef27f6bddda387.png), and the car will follow the obstacle to move.

![](./media/img-20240117093900.png)

