### Project 22: Fire Extinguishing Tank  


#### **(1)Description:**

The line-tracking function of the smart tank has been explained in the previous project. And in this project we use the flame sensor to make a fire extinguishing robot. 

When the car encounters flames, the motor of the fan will rotate to blow out the fire. Of course, we need to replace the ultrasonic sensor and two photoresistors with a fan module and flame sensors first. 

The specific logic of the line-tracking smart car is shown in the table below:

| Left Flame Sensors | Right Flame Sensors | Status                                          |
| :----------------: | :-----------------: | :---------------------------------------------- |
|        ≤700        |        ≤700         | Car stops，fan starts rotating to blow up flame |
|        ≥700        |        ≥700         | Car stops，fan starts rotating to blow up flame |
|        ≥700        |        ≥700         | Car stops，fan starts rotating to blow up flame |
|       ＞700        |        ＞700        | Fan stops，car moves                            |

<span style="color: rgb(255, 76, 65);">**Note:**</span>
1）This experiment requires the use of a fire source. Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. 
2）The flame sensoris not fireproof, please do not burn it directly with flame.
We can control an external LED with the flame sensor. The LED still is connected to D9. When fire is connected, LED will be on.

#### **(2)Flow chart:**

![](media/wps12.png)

#### **(3)Connection Diagram:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

#### **(4)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 22
  Fire extinguishing tank
  http://www.keyestudio.com
*/

int flame_L = A1; //Define the flame interface on the left as the analog pin A1
int flame_R = A2; //Define the flame interface on the right as the analog pin A2
//The wiring of line tracking sensor
#define L_pin  11  //left
#define M_pin  7  //middle
#define R_pin  8  //right
//The pin of the servo 130
int INA = 12;
int INB = 13;
#define ML_Ctrl 4  //Define the direction control pin of the left motor
#define ML_PWM 6   //Define the PWM control pin of the left motor
#define MR_Ctrl 2  //Define the direction control pin of the right motor
#define MR_PWM 5   //Define the PWM control pin of the right motor
int L_val, M_val, R_val, flame_valL, flame_valR;

void setup()
{
  Serial.begin(9600);
  //Set all pins of the line tracking sensor as input mode
  pinMode(L_pin, INPUT);
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);
  //Define the flame as INPUT
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
  //Define the motor as OUTPUT
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  pinMode(INA, OUTPUT);//Set digital port INA as OUTPUT
  pinMode(INB, OUTPUT);//Set digital port INB as OUTPUT
}

void loop () 
{
  //Read the analog value of the flame sensors
  flame_valL = analogRead(flame_L);
  flame_valR = analogRead(flame_R);
  Serial.print(flame_valL);
  Serial.print("  ");
  Serial.print(flame_valR);
  Serial.println("  ");
//  delay(500);
  if (flame_valL <= 700 || flame_valR <= 700) 
  {
    Car_Stop();
    fan_begin();
  } 
  else 
  {
    fan_stop();
    L_val = digitalRead(L_pin); //Read the value of the left sensor
    M_val = digitalRead(M_pin); //Read the value of the middle sensor
    R_val = digitalRead(R_pin); //Read the value of the right sensor
    
    if (M_val == 1)  //the middle one detects black lines
    {
      if (L_val == 1 && R_val == 0)  //If a black line is detected on the left, but not on the right, turn left
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //If a black line is detected on the right, not on the left, turn right
      {
        Car_right();
      }
      else  //otherwise, go front
      {
        Car_front();
      }
    }
    else  //The middle one doesn't detect black lines
    {
      if (L_val == 1 && R_val == 0)  //If a black line is detected on the left, but not on the right, turn left
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1)  //If a black line is detected on the right, not on the left, turn right
      {
        Car_right();
      }
      else  //otherwise, stop
      {
        Car_Stop();
      }
    }
  }
}

void fan_stop() 
{
  //stop rotating
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

void fan_begin() 
{
  //fan rotates
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 150);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 150);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 100);
  
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}
```

#### **(5)Test Result:**

After uploading the test code successfully and powering it up, the smart car puts out the fire when it detects flame and continues moving along the black line.

![](media/694677ab33053846ec588667dc40ecfa.jpeg)

<span style="color: rgb(255, 76, 65);">**Note:**</span>
Please make it away from flammable items to prevent fire. Children should experiment under adult supervision. If you cannot confirm that you are safe, please abandon the experiment. The flame sensor is not fireproof, please do not burn it directly with flame.

