### Project 20: Fan

#### **(1)Description：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

This fan module uses a HR1124S motor-controlling chip, a single-channel H-bridge driver chip containing a low-conductivity resistance PMOS and NMOS power tubes. The low-conducting resistance can ease the power consumption, contributing to the safe work of the chip for longer time.

In addition, its low standby current and low static working current makes itself apply to toys. We can control the rotation direction and speed of the fan by outputting IN + and IN- signals and PWM signals.

#### **(2)Parameters:**

- Working voltage: 5V

- Current: 200mA

- Maximum power: 2W

- Work temperature: -10 ° C to +50 degrees Celsius

- Size: 47.6mm \* 23.8mm

#### **(3)Connection Diagram:**

The fan module needs driving by large current; therefore, we install a battery holder.

![](media/2bd9aa5cc21e274458328958561f1915.png)

The pin GND, VCC, IN+ and IN- of the fan module are connected to pin G, V, 12 and 13 of the shield.

#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/1360090880c1cd9b20671c17604f4108.png)

![](media/4e9354e674060efe6cf540a3e1b87813.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/cbb8f153dd0d114bdd350577af7a1f02.png)

#### **(5)Test Results:**

Upload code, wire up components, power on and turn the DIP switch to ON. The small fan will turn clockwise for 2s, stop for 2s and anticlockwise for 2s

![](./media/img-20240117100504.png)

#### **(6)Extension Practice:**

We have understood the working principle of the flame sensor. Next, hook up a flame sensor in the circuit , as shown below. Then control the fan to blew out fire with the flame sensor.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)


You can drag blocs to edit your code, as shown below

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/74ddb07daf4063f0640c31f4243a0864.png)


After uploading the code, turn on the power switch of the motor drive shield, you can turn on the fan when flame is detected from the left flame sensor of the robot.

![](./media/img-20240117102303.png)
