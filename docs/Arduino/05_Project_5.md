### Project 5: Servo Control

#### **(1)Description:**

A servo motor is a position control rotary actuator. It mainly consists of a housing, a circuit board, a core-less motor, a gear, and a position sensor. Its working principle is that the servo receives the signal sent by the MCU or receiver and produces a reference signal with a period of 20ms and a width of 1.5ms. It then compares the acquired DC bias voltage to the voltage of the potentiometer and obtains the voltage difference output.

When the motor speed is constant, the potentiometer is driven to rotate through the cascade reduction gear, which leads that the voltage difference is 0, and the motor stops rotating. Generally, the angle range of servo rotation is 0° --180 °

The rotation angle of servo motor is controlled by regulating the duty cycle of PWM (Pulse-Width Modulation) signal. The standard cycle of PWM signal is 20ms (50Hz). Theoretically, the width is distributed between 1ms-2ms, but in fact, it's between 0.5ms-2.5ms. The width corresponds to the rotation angle from 0° to 180°. Note that for different brand motors, the same signal may result in different rotation angles.  

![](media/69be958142b773acdae33eeef12afed7.png)

In general, servo has three lines in brown, red and orange. The brown wire is grounded, the red one is a positive pole line and the orange one is a signal line.

![](media/49467dfa70799401a5a5acc691014aee.png)

The angle of the servo:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parameters:**

- Working voltage: DC 4.8V \~ 6V

- Operating angle range: about 180 ° (at 500 → 2500 μsec)

- Pulse width range: 500 → 2500 μsec

- No-load speed: 0.12 ± 0.01 sec / 60 (DC 4.8V) 0.1 ± 0.01 sec / 60 (DC 6V)

- No-load current: 200 ± 20mA (DC 4.8V) 220 ± 20mA (DC 6V)

- Stopping torque: 1.3 ± 0.01kg · cm (DC 4.8V) 1.5 ± 0.1kg · cm (DC 6V)

- Stop current: ≦ 850mA (DC 4.8V) ≦ 1000mA (DC 6V)

- Standby current: 3 ± 1mA (DC 4.8V) 4 ± 1mA (DC 6V)

#### **(3)Connection Diagram:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">Note:</span> The brown, red and orange wire of the servo are respectively attached to Gnd(G), 5v(V) and 10 of the shield. Remember to connect an external power because of the high current of the servo. If not, the development board will be burnt out.

#### **(4)Test Code 1:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.1
Servo
http://www.keyestudio.com
*/

#define servoPin 10 //The pin of servo

int pos; //The variable of servo’s angle
int pulsewidth; //The variable of servo’s pulse width

void setup() 
{
    pinMode(servoPin, OUTPUT); //Set the pin of servo as output
    procedure(0); //Set the angle of servo to 0°
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  // From 1°to 180°
    {
    	// in steps of 1 degree	
        procedure(pos); // Rotate to the angle of 'pos'
        delay(15); //Control the speed of rotation
    }
    for (pos = 180; pos >= 0; pos -= 1) // From 180° to 1°
    { 
        procedure(pos); // Rotate to the angle of 'pos'
        delay(15);
    }
}
//The function controls the servo
void procedure(int myangle) 
{
    pulsewidth = myangle * 11 + 500; //Calculate the value of pulse width
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth); //The time in high level represents the pulse width
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000)); //As the cycle is 20ms, the time left is in low level
}
```

Upload code, we will see the servo move from 0° to 180°. In the further chapters, we will introduce how to drive a servo. Additionally, we can control a servo with a servo library of Arduino.

<span style="color: rgb(255, 76, 65);">Note:</span> This servo library file uses timer 1, and the PWM output of IO ports 9 and 10 also uses timer 1, so we cannot use this servo library when using the PWM output of D9 and D10 later.

#### **(5)Test Code2:**

(<span style="color: rgb(255, 76, 65);">Note: </span> Do not connect the Bluetooth module before uploading the code, because the uploading of the code also uses serial communication, and there may be conflicts with the serial communication of the Bluetooth, which can cause the uploading of the code to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.2
Servo
<http://www.keyestudio.com>
*/

#include <Servo.h>

Servo myservo; // create servos
int pos = 0; // Save the variables of angle

void setup() 
{
	myservo.attach(10); //Connect the servo with digital port 10
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  //From 0° to 180°
    {
    	//step length is 1
        myservo.write(pos); // Rotate to the angle of 'pos'
        delay(15); // Wait for 15ms to control speed
    }

    for (pos = 180; pos >= 0; pos -= 1)  //From 180° to 0°
    {
        myservo.write(pos); // Rotate to the angle of 'pos'
        delay(15); // Wait for 15ms to control speed
    }
}
```

#### **(6)Test Results:**

Upload code, plug in power and servo moves in the range of 0° and 180°.

![](./media/img-20240117090810.png)

#### **(7)Code Explanation:**

Arduino comes with **\#include \<Servo.h\>** (servo function and statement）

The following are some common statements of the servo function:

1\. **attach（interface）**——Set servo interface, port 9 and 10 are available

2\. **write（angle）**——The statement to set rotation angle of servo, the angle range is from 0° to 180°

3\. **read（）**——The statement to read angle of servo, read the command value of “write()”

4\. attached（）——Judge if the parameter of servo is sent to its interface

Note: The above written format is“servo variable name, specific statement（）”, for instance: myservo.attach(10)
