### Project 12: Ultrasonic Obstacle Avoidance Tank

#### **(1)Description:**

In the previous project, we made an ultrasonic sound-following smart car. In fact, using the same components and the same wiring method, we only need to change the test code to turn it into an ultrasonic obstacle avoidance smart car. This smart car can move with the movement of the human hands. 

We use ultrasonic sensors to detect the distance between the smart car and the obstacle in front, and then control the rotation of the two motors based on this data so as to control the movements of the smart car.

|                          Detection                           |         |
| :----------------------------------------------------------: | :-----: |
| Distance measured by the ultrasonic senor between the car and the obstacle in front <br />（set the angle of the servo to 90°） | a (cm)  |
| Distance measured by the ultrasonic senor between the car and the obstacle on the right <br />（set the angle of the servo to 0°） | a2 (cm) |
| Distance measured by the ultrasonic senor between the car and the obstacle on the left <br />（set the angle of the servo to 180°） | a1 (cm) |

**Setting: set the starting angle of the servo to 90°**

| Condition 1 |        Condition 2         |      Condition 3       | Movement                                                     |
| :---------: | :------------------------: | :--------------------: | :----------------------------------------------------------- |
|    a＜20    |                            |                        | Stop for 500ms；set the angle of the servo to 180°，read a1，delay in 100ms；set the angle of the servo to 0°，read a2，delay in 0.1s. |
|             | a1＜50<br />or<br />a2＜50 | **Compare a1 with a2** |                                                              |
|             |                            |         a1＞a2         | Set the angle of the servo to 90°，rotate left for 700ms（set PWM to 255），and move forward（set PWM to 200）. |
|             |                            |         a1＜a2         | Set the angle of the servo to 90°，rotate right for 700ms（set PWM to 255），and move forward（set PWM to 200）. |
|             | a1≥50<br />and<br />a2≥50  |         Random         | set the angle of the servo to 90°，rotate left for 500ms（set PWM to 255），and move forward（set PWM to 200）.<br /><br />set the angle of the servo to 90°，rotate right for 500ms（set PWM to 255），and move forward（set PWM to 200）. |
|    a≥20     |                            |                        | move forward（set PWM to 100）                               |

#### **(2)Flow chart:**

![](media/wps119.png)

#### **(3)Connection Diagram:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

(<span style="color: rgb(255, 76, 65);">Note:</span> the brown, red and orange wires of the servo are respectively connected to G (GND), V（5V）and D10 of the expansion board；and for the ultrasonic sensor, the VCC pin is connected to the 5v (V) ,the Trig pin to digital 12 (S), the Echo pin to digital 13 (S), and the Gnd pin to Gnd (G); the same as last project.）

#### **(4)Test Code:**


You can also drag blocks to edit your code, as shown below.![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/5dcbd405806b8e341505d7316246dbdd.png)

（3）![](media/996c8d4e5dd9620757dfb097329e7d5d.png)

（4）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

（10）![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

（11）![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/4360f9642a8c6b2488767c079d481482.png)

#### **(5)Test Results:**

After uploading the test code successfully, wire it up, turn the DIP switch to the ON end, and power up. The smart car will move forward and automatically avoid obstacles.

![](./media/img-20240117093950.png)

