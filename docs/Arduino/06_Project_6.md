### Project 6: Ultrasonic Sensor

#### **(1) Description:**

![](media/0180b169a1c3b228394b43df704fac32.png)

The HC-SR04 ultrasonic sensor uses sonar to determine distance to an object like what bats do. It offers excellent non-contact range detection with high accuracy and stable readings in an easy-to-use package. It comes complete with ultrasonic transmitter and receiver modules.

The HC-SR04 or the ultrasonic sensor is being used in a wide range of electronics projects for creating obstacle detection and distance measuring application as well as various other applications. Here we have brought the simple method to measure the distance with Arduino and ultrasonic sensor and how to use ultrasonic sensor with Arduino.

![](./media/image-20250709105712919.png)

#### **(2)Parameters:**

- Power Supply :+5V DC

- Quiescent Current : \<2mA

- Working Current: 15mA

- Effectual Angle: \<15°

- Ranging Distance : 2cm – 400 cm

- Resolution : 0.3 cm

- Measuring Angle: 30 degree

- Trigger Input Pulse width: 10uS


#### **(3) The principle of ultrasonic sensor:**

As the above picture shown, it is like two eyes. One is transmitting end, the other is receiving end.

The ultrasonic module will emit the ultrasonic waves after triggering a signal. When the ultrasonic waves encounter the object and are reflected back, the module outputs an echo signal, so it can determine the distance of the object from the time difference between the trigger signal and echo signal. 

The t is the time that emitting signal meets obstacle and returns. And the propagation speed of sound in the air is about 343m/s, and distance = speed * time. However, the ultrasonic wave emits and comes back, which is 2 times of distance. Therefore, it needs to be divided by 2, the distance measured by **ultrasonic wave = (speed * time)/2**

1. Use method and timing chart of ultrasonic module:

2. Setting the delay time of Trig pin of SR04 to 10μs at least, which can trigger it to detect distance.

3. After triggering, the module will automatically send eight 40KHz ultrasonic pulses and detect whether there is a signal return. This step will be completed automatically by the module.

4. If the signal returns, the Echo pin will output a high level, and the duration of the high level is the time from the transmission of the ultrasonic wave to the return.

![](media/image-20230426172540424.png)

Circuit diagram of ultrasonic sensor:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4)Connection Diagram:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Note:</span> The pin VCC, Trig, Echo and Gnd of the ultrasonic sensor are respectively connected to 5v(V), 12(S), 13(S) and Gnd(G) of the shield.

#### **(5)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.1
Ultrasonic sensor
http://www.keyestudio.com
*/

int trigPin = 12; // Pin Trig attaches to 12
int echoPin = 13; //Pin Echo attaches to 13
long duration, cm, inches;

void setup() 
{
    //Serial Port begin
    Serial.begin(9600);//Set the baud rate to 9600
    //Define input and output
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
}

void loop() 
{
    //Pre-given a short low pulse to ensure a clean high pulse
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);//At least give 10us high level trigger
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // The time in high level equals the time gap between the transmission and the return of the ultrasonic sound
    duration = pulseIn(echoPin, HIGH);
    // Translate into distance
    cm = (duration / 2) / 29.1; // convert to centimeters
    inches = (duration / 2) / 74; // Convert to inch
    //serial port prints out
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    delay(50);
}
```

#### **(6)Test Results:**

Upload the test code to the development board, open the serial monitor, and set the baud rate to 9600. The detected distance will be displayed in cm and inches. When you hinder the ultrasonic sensor with your hand, the displayed distance value will get smaller.

![](media/2ff018e5d9d631a32fce99eb9b4778be.png)

#### **(7)Code Explanation:**

**int trigPin = 12;**  this pin is defined to transmit ultrasonic waves, generally output.

**int echoPin = 13;** this is defined as the pin of reception, generally input

**cm = (duration/2) / 29.1; inches = (duration/2) / 74; by 0.0135**

We can calculate the distance by using the following formula:

distance = (traveltime/2) x speed of sound

The speed of sound is: 343m/s = 0.0343 cm/uS = 1/29.1 cm/uS

Or in inches: 13503.9in/s = 0.0135in/uS = 1/74in/uS

We need to divide the traveltime by 2 because we have to take into account that the wave was sent, hit the object, and then returned back to the sensor.

#### **(8)Extension Practice:**


We have just measured the distance displayed by the ultrasonic. How about controlling the LED with the measured distance? Let's try it and connect an LED light module to the D9 pin.

![](media/291ac1db0f38418772d11bb1786b7314.png)

**Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.2
Ultrasonic LED
http://www.keyestudio.com
*/

int trigPin = 12; // Trig is connected to 12
int echoPin = 13; // Echo is connected to 13
int LED = 9;
long duration, cm, inches;

void setup() 
{
    //start serial port
    Serial.begin (9600);//set baud rate to 9600
    //define input and output
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LED, OUTPUT);
}

void loop() 
{
    //Pre-given a short low pulse to ensure a clean high pulse
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);//Give at least 10us high level trigger
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // The duration of the high level is the time from the launch to the return of the ultrasonic wave
    duration = pulseIn(echoPin, HIGH);
    // convert to distance
    cm = (duration / 2) / 29.1; // convert to centimeters
    inches = (duration / 2) / 74; // convert to inches
    //serial port prints out
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    if (cm >= 2 && cm <= 10) 
    {
    	digitalWrite(LED, HIGH);//turn on LED
    } 
    else 
    {
    	digitalWrite(LED, LOW); //turn off LED
    }
    delay(50);
}
```

Upload test code to development board and block ultrasonic sensor by hand, then check if LED is on.

![](./media/img-20240117090734.png)
