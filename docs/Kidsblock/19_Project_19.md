### Project 19: Flame Sensor

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Description:**

The flame sensor uses an IR receiving tube to detect flames. It converts the brightness of the flame into high and low-level signals and inputs them into the central processor for corresponding program processing. The voltage value of the analog port varies depending on whether there is a flame close by or no flame at all.

If there is no flame, the analog port reads about 0.3V; when there is a flame, the analog port reads about 1.0V. The closer the flame is, the higher the voltage value. It can be used to detect a fire source or to build a smart robot.

Note that the probe of the flame sensor can only withstand temperatures between -25℃ and 85℃.

During use, make sure to keep the flame sensor at a safe distance from the fire to avoid damaging it.

#### **(2)Parameters:**

![](media/e2c77a94067ccd3e634fb3674c02b80f.png)

- Working voltage: 3.3V-5V (DC)

- Current: 100mA

- Maximum power: 0.5W

- Work temperature: -10 ° C to +50 degrees Celsius

- Sensor size: 31.6mmx23.7mm

- Interface: 4pin turn 3PIN interface

- Output signal: analog signals A0, A1

#### **(3)Connection Diagram:**

![](media/10f5f2256c61c54bf7f9a7a0c52375f9.png)

Pin A of two photoresistors are connected to A1 and A2. We connect the flame sensor to A1 and A2. We replace two photoresistors and the ultrasonic sensor with two flame sensors and a fan, an extinguishing car is created.

<span style="color: rgb(255, 76, 65);">**Note:**</span>
1）This experiment requires the use of a fire source. Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. 
2）**The flame sensoris not fireproof, please do not burn it directly with flame.**

#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/4bc6c8a4d6e964fd078a6aeb0dd51ff4.png)

#### **(5)Test Results:**

Wire up components, burn the code, open the serial monitor and set the baud rate to 9600.

You can view the simulation value of flame sensor.

The closer the flame, the smaller the simulation value.

Adjust the potentiometer on the module to maintain the LED at the critical point. When the sensor does not detect flame, the LED will be off, but if the sensor detects flame, the LED will be on.

![](./media/img-20240117100139.png)

![](media/60d0ce2044a504135af3b1113a1a4c7d.png)

#### **(6)Extension Practice:**

<span style="color: rgb(255, 76, 65);">**Note:**</span>
1）This experiment requires the use of a fire source. Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. 
2）The flame sensoris not fireproof, please do not burn it directly with flame.
We can control an external LED with the flame sensor. The LED still is connected to D9. When fire is connected, LED will be on.

![](media/814c315d3bb44278b476a754d3681227.png)

You can drag blocs to edit your code, as shown below

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/9d2f5915e4a6991ed4549b39ec853fa5.png)

You can use the flame of a lighter near the left flame sensor. When the flame sensor detects a flame, the LED module will light up as an alarm.

![](./media/img-20240117100333.png)

<span style="color: rgb(255, 76, 65);">**Note:**</span>
Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. The flame sensor is not fireproof, please do not burn it directly with flame.

