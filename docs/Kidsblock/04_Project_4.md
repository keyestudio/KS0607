### Project 4: Line Tracking Sensor

#### **(1)Description:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

The tracking sensor is actually an infrared sensor. The component used here is the TCRT5000 infrared tube.

Its working principle is to use different reflectivity of infrared light to colors, then convert the strength of the reflected signal into a current signal.

During the process of detection, black is active at HIGH level while white is active at LOW level. The detection height is 0-3 cm.

Keyestudio 3-channel line tracking module has integrated 3 sets of TCRT5000 infrared tube on a single board, which is more convenient for wiring and control.

If the Line Tracking Sensor does not work as expected, you will need to use a screwdriver to adjust its potentiometerto make it more sensitive. When yourfinger is close to the sensor, its on-board LED light turns on, and when yourfinger moves away, its on-board LED light turns off. At thistime, itssensitivity isrelatively good.

![](./media/img-20240117091947.png)

#### **(2)Parameters:**

- Operating Voltage: 3.3-5V (DC)
- Interface: 5PIN
- Output Signal: Digital signal
- Detection Height: 0-3 cm

Special note: before testing,rotate the potentiometer on the sensor to adjust the detection sensitivity. When adjust the LED at the threshold between ON and OFF, the sensitivity is the best.

<span style="color: rgb(255, 76, 65);">Note:</span> the line tracking sensor is installed under the bottom of the robot.

#### **(3)Connection Diagram:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/700cb0ecc14cbccd6e367c5098360f08.png)

![](media/271423c55b5f147796beb344eed7e9cf.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/5298cdfb6fd7c71df155c969c80450cd.png)

#### **(5)Test Results:**

Upload the code to the development board, open serial monitor to 9600 and check line tracking sensors. And the displayed value is 1(high level) when no signals are received. The value shifts into 0 when the sensor is covered with paper.

![](media/5630032421adf9446d51b770f0e7f8af.png)

#### **(6)Extension Practice:**

We can control an LED with this sensor. The LED is connected to D9. If we cover it , the LED will light up.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

You can also drag blocks to edit your code, as shown below.

![](media/5ad9eb9c639b74f8271a55079dcf845c.png)

![](media/b1e2059ec06fcfc9423fa6287eb998ef.png)

![](media/574854f4d96c40a85e1db549d85f14f4.png)

![](media/9077c0d059f7a4d3277f10ccb4e962fb.png)

![](media/1a6838765472e3cd3836abb5202d9ab1.png)

![](media/80e9c514357c63f4791c72220829b673.png)

![](media/b10e1897e99af2c1ade6c09da6c30dba.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/b5a4b5a04cdee9f79d6e18a5c48cbe48.png)

When an object (such as paper or a finger) approaches the line-following sensor, the sensor detects the return signal emitted by itself, and the LED module lights up. When the sensor does not detect any return signal, the LED module turns off.

![](./media/img-20240117092116.png)
