### Project 13: Move-in-Confined-Space Tank


#### **(1)Description:**

The ultrasonic sound-following and obstacle avoidance functions of the smart car have been introduced in previous projects. Here we intend to combine the knowledge in the previous courses to confine the smart car to  move in a certain space. 

In the experiment, we use the line-tracking sensor to detect whether there is a black line around the smart car, and then control the rotation of the two motors according to the detection results, so as to lock the smart car in a circle drawn in black line.

The specific logic of the line-tracking smart car is shown in the table blow:

![](./media/image-20250709112523897.png)

|                         Condition                         |                         Movement                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| If one of three line tracking sensors detects black lines | Go back（set PWM to 150）Then turn left（set PWM to 150） |
|             None of them detects black lines              |               Go forward（set PWM to 100）                |

#### **(2)Flow chart:**

![](media/image-20230427092708208.png)

#### **(3)Connection Diagram:**

![](media/e5c3763e764359ec8be92102b6d2a7f9.png)

#### **(4)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 13
  draw a circle for tank
  http://www.keyestudio.com
*/

//The wiring of line tracking sensor
#define L_pin  11  //left
#define M_pin  7  //middle
#define R_pin  8  //right

#define ML_Ctrl 4  //Define the direction control pin of the left motor
#define ML_PWM 6   //Define the PWM control pin of the left motor
#define MR_Ctrl 2  //Define the direction control pin of the right motor
#define MR_PWM 5   //Define the PWM control pin of the right motor
int L_val, M_val, R_val;

void setup()
{
  Serial.begin(9600); //Set the baud rate to 9600
  pinMode(L_pin, INPUT); //Set all pins of the line tracking sensor as input mode
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
}

void loop () 
{
  L_val = digitalRead(L_pin); //Read the value of the left sensor
  M_val = digitalRead(M_pin); //Read the value of the middle sensor
  R_val = digitalRead(R_pin); //Read the value of the right sensor
  if ( L_val == 0 && M_val == 0 && R_val == 0 )  //when black lines are not detected, go front
  {
    Car_front();
  }
  else  //black lines are detected, go back then turn left
  {
    Car_back();
    delay(700);
    Car_left();
    delay(800);
  }
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 150);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Test Results:**

After uploading the test code successfully and powering it up, the smart car moves in a confined space, the circle drawn in black line.

![](./media/img-20240117090340.png)
