### Project 13: Move-in-Confined-Space Tank


#### **(1)Description:**

The ultrasonic sound-following and obstacle avoidance functions of the smart car have been introduced in previous projects. Here, we intend to combine the knowledge from the previous courses to confine the smart car to move within a certain space. In the experiment, we use the line-tracking sensor to detect whether there is a black line around the smart car, and then control the rotation of the two motors according to the detection results, so as to lock the smart car in a circle drawn with a black line.

The specific logic of the smart car is shown in the table below:

![](media/image-20230525114604923.png)

|                         Condition                         |                         Movement                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| If one of three line tracking sensors detects black lines | Go back（set PWM to 150）Then turn left（set PWM to 150） |
|             None of them detects black lines              |               Go forward（set PWM to 100）                |

#### **(2)Flow chart**

![](media/b3c30f92cb78d4c2a4a8bd746aef24e1.png)

#### **(3)Connection Diagram:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/e48288f5b46e3e1c78489cb9d9b86333.png)

（3）![](media/801d176b32bc87904b8545ecf80874fc.png)

（4）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/b919eb2b47ee87ae36e21099e754e8a1.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/e656126c11bb8ebe7b6b0df8f22e7a79.png)

#### **(5)Test Results:**

After uploading the test code successfully and powering up, the smart car moves in a circle drawn with a black line.

![](./media/img-20240117094034.png)
