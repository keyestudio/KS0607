### Project 10: Light Following Tank


#### **(1)Description:**

In previous projects, we introduced in detail the use of various sensors, modules, and expansion boards on the smart car. Now let’s move to the projects of the smart car . The light-following smart cars, as the name suggests, is a smart car that can follow the light.

We can combine the knowledge from projects photoresistor and motor drive to make a light-seeking smart car. In the project, we use two photoresistor modules to detect the light intensity on the left and right sides of the smart car, read the corresponding analog values, and then control the rotation of the two motors based on these two data so as,to control the movements of the smart car.

The specific logic of the light-following smart car is shown as below.

![](./media/image-20250709111733042.png)

#### **(2)Flow chart:**

![](media/wps8.png)

#### **(3)Connection Diagram:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Note:</span> The pin "G", "V" and S of the left photoresistor module are connected to G (GND), V (VCC), A1 respectively;

The pin "G", "V" and S of the right photoresistor module are connected to the G (GND), V (VCC), and A2 respectively.

The 4pin cable is marked with A, A1, B1 and B. The right rear motor is connected to B port of the 8833 motor driver expansion board and the left front motor is connected to A port of the 8833 motor driver expansion board

#### **(4)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 10
  light follow tank
  http://www.keyestudio.com
*/
#define light_L_Pin A1   //Define the pin of the photosensitive sensor on the left
#define light_R_Pin A2   //Define the pin of the photosensitive sensor on the right
#define ML_Ctrl 4  //Define the direction control pin of the left motor
#define ML_PWM 6   //Define the PWM control pin of the left motor
#define MR_Ctrl 2  //Define the direction control pin of the right motor
#define MR_PWM 5   //Define the PWM control pin of the right motor
int left_light;
int right_light;
void setup() 
{
  Serial.begin(9600);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop() 
{
  left_light = analogRead(light_L_Pin);
  right_light = analogRead(light_R_Pin);
  Serial.print("left_light_value = ");
  Serial.println(left_light);
  Serial.print("right_light_value = ");
  Serial.println(right_light);
  if (left_light > 650 && right_light > 650) //go front
  {
    Car_front();
  }
  else if (left_light > 650 && right_light <= 650)  //turn left
  {
    Car_left();
  }
  else if (left_light <= 650 && right_light > 650) //turn right
  {
    Car_right();
  }
  else  //otherwise, stop
  {
    Car_Stop();
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
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
```

#### **(5)Test Result**

After uploading the test code successfully, connecting according to the wiring diagram, dialing the DIP switch to the right end and powering it on, the smart car follows the light to move.

![Img](./media/img-20240117090537.png)
