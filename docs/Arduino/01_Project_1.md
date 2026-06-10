### Project 1: LED Blinks

#### **(1)Description:**

![](media/64b0b431d58473408ac46b39d2dc2ad0.jpeg)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

For starters and enthusiasts, LED Blink is a fundamental program. LED, the abbreviation of light emitting diodes, consists of Ga, As, P, N chemical compounds and so on. The LED can flash in diverse colors by altering the delay time in the test code. When in control, power on GND and VCC. The LED will be on if the S end is at a high level; otherwise, it will go off.

#### **(2)Parameters:**

![](./media/image-20250709104606457.png)

- Control interface: digital port
- Working voltage: DC 3.3-5V
- Pin spacing: 2.54mm
- LED display color: yellow

#### **(3)Components Required:**

![](media/img-20240117081416.png)


#### **(4)8833 Motor driver expansion board:**

The Keyestudio 8833 motor driver expansion board is compatible with the Arduino UNO development board. Just stack it onto the development board when using it.

![](./media/image-20250709104749140.png)

#### **(5)Connection Diagram:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](media/d68e6475a7c9ed55bb057b75d1b11689.png)

<span style="color: rgb(255, 76, 65);">**NOTE:**</span> The LED is connected to the D9 port. Remember to install jumper caps onto the shield.

#### **(6)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.1

Blink

http://www.keyestudio.com

*/

int LED = 9; //Define the pin of LED to connect with digital port 9

void setup()
{
	pinMode(LED, OUTPUT); //Initialize the LED pin to output mode
}

void loop() //infinite loop
{
	digitalWrite(LED, HIGH); //Output high level and turn on the LED
	delay(1000); //Wait for 1s
	digitalWrite(LED, LOW); //Output low level and turn off the LED
	delay(1000); //Wait for 1s
}
```

#### **(7)Test Results:**

Upload the program, LED blinks at the interval of 1s.

#### **(8)Code Explanation:**

**pinMode(LED，OUTPUT) -** This function can denote that the pin is INPUT or OUTPUT

**digitalWrite(LED，HIGH) -** When pin is OUTPUT, we can set it to HIGH(output 5V) or LOW(output 0V)

#### **(9)Extension Practice:**

We have succeeded in blinking LED. Next, let’s observe what will happen to the LED if we modify pins and delay time.

**Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.2

Blink

http://www.keyestudio.com

*/

int LED = 9; //Define the pin of the LED as 9

void setup()
{
	pinMode(LED, OUTPUT); //Set the pin of the LED to OUTPUT
}

void loop() //Infinite loop
{
    digitalWrite(LED, HIGH); //output high levels, light up LED
	delay(100); //Wait for 0.1s
	digitalWrite(LED, LOW); //LED output low levels, turn off LED
	delay(100); //Wait for 0.1s

}
```

The test result shows that the LED flashes faster. Therefore, we can draw a conclusion that pins and time delaying affect flash frequency.
