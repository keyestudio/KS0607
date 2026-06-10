### Project 20: Flame Sensor

![](media/7cf8c051f489b06119c262cd059c23c5.jpeg)

#### **(1)Description：**

The flame sensor uses an IR receiving tube to detect flames. It converts the brightness of the flame into high and low-level signals and inputs them into the central processor for corresponding program processing. The voltage value of the analog port varies depending on whether there is a flame close by or no flame at all.

If there is no flame, the analog port reads about 0.3V; when there is a flame, the analog port reads about 1.0V. The closer the flame is, the higher the voltage value. It can be used to detect a fire source or to build a smart robot.

Note that the probe of the flame sensor can only withstand temperatures between -25℃ and 85℃.

During use, make sure to keep the flame sensor at a safe distance from the fire to avoid damaging it.

#### **(2)Parameters：**

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

Flame sensors are connected to A1 and A2. 

When we remove ultrasonic sensors and photoresistors, then add flame sensors and fan modules.
The fire extinguishing robot is created.

<span style="color: rgb(255, 76, 65);">**Note:**</span>
1）This experiment requires the use of a fire source. Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. 
2）**The flame sensoris not fireproof, please do not burn it directly with flame.**


#### **(4)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.1

flame sensor

http://www.keyestudio.com

*/

int flame = A1; //Define the flame pin as analog pin A1
int val = 0; //Define digital variables

void setup() 
{
	pinMode(flame, INPUT); //Define the buzzer as an input source
    Serial.begin(9600); //Set the baud rate to 9600
}

void loop() 
{
	val = analogRead(flame); //Read the analog value of the flame sensor
	Serial.println(val);//Output analog value and print it
	delay(100); //Delay in 100ms
}
```

#### **(5)Test Result：**

Wire up components, burn the code, open the serial monitor and set the baud rate to 9600.

You can view the simulation value of flame sensor.

The closer the flame, the smaller the simulation value.

Adjust the potentiometer on the module to maintain D1 at the critical point. When the sensor does not detect flame, the D1 will be off, but if the sensor detects flame, the D1 will be on.

![](./media/img-20240117085629.png)

![](media/05db06b3e205dfca63c2ba3aa7ff528e.png)

<span style="color: rgb(255, 76, 65);">**Note:**</span>
Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. The flame sensor is not fireproof, please do not burn it directly with flame.

#### **(6)Extension Practice:**

<span style="color: rgb(255, 76, 65);">**Note:**</span>
1）This experiment requires the use of a fire source. Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. 
2）The flame sensoris not fireproof, please do not burn it directly with flame.

Next, connect an LED to pin 9 and we can control it by a flame sensor, as shown below;

![](media/814c315d3bb44278b476a754d3681227.png)

**Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 20.2

flame sensor

http://www.keyestudio.com

*/

int flame = A1; //Define the flame pin as analog pin A1
int LED = 9; //Define the LED as digital port 9
int val = 0; //Define digital variables

void setup() 
{
    pinMode(flame, INPUT); //Define the flame as an input source
    pinMode(LED, OUTPUT); //Set LED to output mode
    Serial.begin(9600); //Set the baud rate to 9600
}

void loop() 
{
    val = analogRead(flame); //Read the analog value of the flame sensor
    Serial.println(val);//Output analog value and print it
    if (val < 300)  //When analog value is less than 300, LED is on
    {
    	digitalWrite(LED, HIGH); //LED is on
    } 
    else 
    {
    	digitalWrite(LED, LOW); //LED is off
    }
    delay(50); //Delay in 50ms
}
```

#### **(8)Test Results：**

You can use the flame of a lighter near the left flame sensor. When the flame sensor detects a flame, the LED module will light up as an alarm.

![](./media/img-20240117085131.png)

<span style="color: rgb(255, 76, 65);">**Note:**</span>
Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. The flame sensor is not fireproof, please do not burn it directly with flame.
