### Project 14:Line-tracking Tank


#### **(1)Description:**

The previous project introduced how to confine the smart car to move within a certain space. In this project, we will use the knowledge learned before to make it a line-tracking smart car. In the experiment, we use the line-tracking sensor to detect whether there is a black line around the smart car, and then control the rotation of the two motors according to the detection results, so as to make the smart car move along the black line.

The specific logic of the smart car is shown in the table below:

|               Sensor               |                          Detection                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Line-tracking sensor in the middle | Black line detected: in high level<br />White line detected: in low level |
|  Line-tracking sensor on the left  | Black line detected: in high level<br />White line detected: in low level |
| Line-tracking sensor on the right  | Black line detected: in high level<br />White line detected: in low level |

|                         Condition 1                          |                         Condition 2                          |   Movement   |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------: |
| Line-tracking sensor <br />in the middle <br />detects the black line | Line-tracking sensor on the left detects the black line<br />the one on the right detects white lines | Rotate left  |
| Line-tracking sensor <br />in the middle <br />detects the black line | Line-tracking sensor on the left detects white lines<br />the one on the right detects the black line | Rotate right |
| Line-tracking sensor <br />in the middle <br />detects the black line | Both the left and right  line-tracking sensors detect white lines<br />Both the left and right line-tracking sensors detect  the black line | Move forward |
| Line-tracking sensor<br />in the middle <br />detects white lines | Line-tracking sensor on the left detects the black line<br />the one on the right detects white lines | Rotate left  |
| Line-tracking sensor<br />in the middle <br />detects white lines | Line-tracking sensor on the left detects white lines<br />the one on the right detects the black line | Rotate right |
| Line-tracking sensor<br />in the middle <br />detects white lines | Both the left and right  line-tracking sensors detect white lines<br />Both the left and right line-tracking sensors detect  the black line |     Stop     |

#### **(2)Flow chart:**

![](media/wps11.png)

#### **(3)Connection Diagram:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

（7）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（8）![](media/fec93c7b8b089de709fd50575931519c.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/294ae4c01072e34b58a334912c90083a.png)


#### **(5)Test Results:**

After uploading the test code successfully and powering on, the smart car moves along the black line.

![](./media/img-20240117094129.png)
