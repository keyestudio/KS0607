### Project 12: Ultrasonic Obstacle Avoidance Tank

![](./media/image-20250709112200577.png)


#### **(1)Description:**

In the previous project, we made an ultrasonic sound-following smart car. In fact, using the same components and the same wiring method, we only need to change the test code to turn it into an ultrasonic obstacle avoidance smart car. This smart car can move with the movement of the human hands. 

We use ultrasonic sensors to detect the distance between the smart car and the obstacle in front, and then control the rotation of the two motors based on this data so as to control the movements of the smart car.

|                          Detection                           |        |
| :----------------------------------------------------------: | :----: |
| Distance measured by the ultrasonic senor between the car and the obstacle in front <br />（set the angle of the servo to 90°） | a(cm)  |
| Distance measured by the ultrasonic senor between the car and the obstacle on the right <br />（set the angle of the servo to 20°） | a2(cm) |
| Distance measured by the ultrasonic senor between the car and the obstacle on the left <br />（set the angle of the servo to 160°） | a1(cm) |
|   **Setting:** set the starting angle of the servo to 90°    |        |

|   Condition 1   |        Condition 2         | Condition 3 | Movement                                                     |
| :-------------: | :------------------------: | ----------- | ------------------------------------------------------------ |
|      a＜20      |                            |             | Stop for 500ms；<br />set the angle of the servo to 180°, read a1, delay in 100ms；<br />set the angle of the servo to 0°, read a2, delay in 0.1s. |
|                 | a1＜50<br />or<br />a2＜50 |             | Compare a1 with a2                                           |
|                 |                            | a1＞a2      | Set the angle of the servo to 90°, rotate left for 700ms (set PWM to 255)<br />move forward（set PWM to 200）. |
|                 |                            | a1＜a2      | Set the angle of the servo to 90°, rotate right for 700ms(set PWM to 255) <br />move forward（set PWM to 200）. |
| **Condition 1** |      **Condition 2**       |             | **Movement**                                                 |
|      a＜20      | a1≥50<br />and<br />a2≥50  | Random      | set the angle of the servo to 90°, rotate left for 500ms(set PWM to 255)<br />move forward(set PWM to 200)<br /><br />set the angle of the servo to 90°, rotate right for 500ms(set PWM to 255) <br />move forward(set PWM to 200) |
|  **Condition**  |                            |             | **Movement**                                                 |
|      a≥20       |                            |             | move forward(set PWM to 100)                                 |



#### **(2)Flow chart:**

![](media/wps10.png)

#### **(3)Connection Diagram:**

![](media/72a10097d286bc5f9589df031b60484a.png)

(<span style="color: rgb(255, 76, 65);">Note:</span> the brown, red and orange wires of the servo are respectively connected to G (GND), V（5V）and D10 of the expansion board；and for the ultrasonic sensor, the VCC pin is connected to the 5v (V) ,the Trig pin to digital 12 (S), the Echo pin to digital 13 (S), and the Gnd pin to Gnd (G); the same as last project.）

#### **(4)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 12
  Ultrasonic avoid tank
  http://www.keyestudio.com
*/
#define servoPin 10  //The pin of servo
int a, a1, a2;
#define ML_Ctrl 4  //Define the direction control pin of the left motor
#define ML_PWM 6   //Define the PWM control pin of the left motor
#define MR_Ctrl 2  //Define the direction control pin of the right motor
#define MR_PWM 5   //Define the PWM control pin of the right motor
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  Serial.begin(9600);
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //Set the angle of the servo to 90°
  delay(500); //delay in 500ms
}

void loop() 
{
  a = checkdistance();  //Assign the distance to the front detected by ultrasonic sensor to the variable a

  if (a < 20) //When the distance to the front is less than 20cm
  {
    Car_Stop();  //The robot stops
    delay(500); //delay in 500ms
    procedure(180);  //Ultrasonic pan-tilt turns left
    delay(500); //delay in 500ms
    a1 = checkdistance();  //Assign the distance to the left detected by ultrasonic sensor to the variable a1
    delay(100); //read value
    procedure(0); //Ultrasonic pan-tilt turns right
    delay(500); //delay in 500ms
    a2 = checkdistance(); //Assign the distance to the right detected by ultrasonic sensor to the variable a2
    delay(100); //read value
    
    procedure(90);  //Back to 90°
    delay(500);
    if (a1 > a2) 
    { //When the distance to the left is bigger than to the right
      Car_left();  //The robot turns left
      delay(700);  //turn left 700ms
    } 
    else 
    {
      Car_right(); //It turns left for 700ms
      delay(700);
    }
  } 
  else//When the distance to the front is >=20c，the robot moves forward
  {    
    Car_front(); //go front
  }

}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}

//The function controls servos
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Calculate the value of pulse width
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //The time in high level represents the pulse width
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //As the cycle is 20ms, the time left is in low level
  }
}

//The function controls ultrasonic sound
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //The 58.20 here comes from 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5)Test Result:**

After upload the test code successfully, wire up, turn the DIP switch to the ON end, and power up, the smart car moves forward and automatically avoids obstacles.

![](./media/img-20240117090420.png)
