### Project 17: Bluetooth Control Tank


#### **(1)Description:**

We have learned the basic knowledge of Bluetooth in the previous project . In this lesson, we will use Bluetooth to control the smart car. Since it involves Bluetooth, a sending end and a receiving end are needed. In the project, we use the mobile phone as the sender (master), and the smart car connected with the HM-10 Bluetooth module (slave) as the receiver.

We have learned earlier that sending a bit can control LEDs. And the principle of controlling this robot car is the same.

We first understand the function of each button on the APP, and then use the button on the APP to control the tank.

#### **(2)Key Function on the APP**

The following table illustrates the functions of corresponding keys:

|                      KEYS                       | FUNCTIONS                                                    |
| :---------------------------------------------: | ------------------------------------------------------------ |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) | Pair and connect HM-10 Bluetooth module; click again to disconnect |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) | select the robot to operate                                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) | to control the movements of the robot by buttons             |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) | To control the movements of the robot by joystick            |
| ![](media/3ab61154b4ae730a3757f40171846825.png) | To control the movements of the robot by gravity             |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) | Send “F”when pressed and “S”when released<br />The car moves forward when it is pressed and stops when released |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) | Send “L”when pressed and “S”when released <br />The car turns left when it is pressed tight and stops when released |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) | Send “R”when pressed and “S”when released<br />The car turns right when it is pressed tight and stops when released |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) | Send “B”when pressed and “S”when released<br />The car turns back when it is pressed tight and stops when released |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) | Send “u”+digit+“\#”when dragged<br />Drag to change the speed of the left motor |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) | Send “v”+digit+“\#”when dragged<br />Drag to change the speed of the right motor |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) | Select to enter Function page                                |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Send “G”when pressed and “S”when pressed again<br />Enter obstacle avoidance mode when pressed and exit when pressed again |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Send “h”when pressed and “S”when pressed again<br />Enter following mode when pressed and exit when pressed again |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Send “e”when pressed and “S”when pressed again<br />Enter line-tracking mode when pressed and exit when pressed again |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Send “f”when pressed and “S”when pressed again<br />Enter move-in-confined-space mode when pressed and exit when pressed again |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Send “i”when pressed and “S”when pressed again<br />Enter light following mode when pressed and exit when pressed again |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Send “j”when pressed and “S”when pressed again<br />Enter fire extinguishing mode when pressed and exit when pressed again |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Select to enter facial expression display mode               |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Send “k”when pressed and “z”when pressed again<br />Show smiling pattern when clicked and clear expression when clicked again |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Send “l”when pressed and “z”when pressed again<br />Show disgusting pattern when clicked and clear expression when clicked again |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Send “m”when pressed and “z”when pressed again<br />Show happy face when clicked and clear expression when clicked again |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Send “n”when pressed and “z”when pressed again<br />Show sad pattern when clicked and clear expression when clicked again |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Send “o”when pressed and “z”when pressed again<br />Show disparaging pattern when clicked and clear expression when clicked again |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Send “p”when pressed and “z”when pressed again<br />Show heart-shaped pattern when clicked and clear expression when clicked again |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) | Choose to enter the custom function interface; there are six keys 1,2,3,4,5,6; with these keys, you can expand some functions by yourself |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) | Click to send “w”<br />Click to display the analog value detected by the photoresistor on the left |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) | Click to send“y”<br />Click to display the analog value detected by the photoresistor on the right |
| ![](media/a76df707b84409e57a1167889c3510d9.png) | Click to send“x” <br />Click to show the distance detected by ultrasonic sensor (unit: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Click to send“c” Click again to send“d”<br />Press to turn on the fan and press again to turn off it |

#### **(3)Flow Chart:**

![](media/image-20230427101759352.png)

#### **(4)Wiring Diagram:**

![](media/930a8024364e07505e845624a94c27bd.png)

The GND, VCC, SDA, and SCL of the 8x16 LED dot matrix are respectively connected to-(GND), + (VCC), SDA, SCL of the expansion board;

The STATE and BRK pins of the Bluetooth module do not need to be connected.

#### **(5)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> When uploading the code, the Bluetooth module must be unplugged, and the Bluetooth can be reconnected after the uploading process. Otherwise, the code may not be uploaded successfully.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 17.
  bluetooth Control tank
  http://www.keyestudio.com
*/

//Array, used to save data of images, can be calculated by yourself or gotten from modulus tool
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  //设Set the clock pin as A5
#define SDA_Pin  A4  //Set the data pin as A4

#define ML_Ctrl 4  //Define the direction control pin of the left motor
#define ML_PWM 6   //Define the PWM control pin of the left motor
#define MR_Ctrl 2  //Define the direction control pin of the right motor
#define MR_PWM 5   //Define the PWM control pin of the right motor
char ble_val;      //Used to store the value obtained by Bluetooth

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); //clear screens
  matrix_display(start01);  //show the image to start
}

void loop() 
{
  if (Serial.available())
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
  }
  switch (ble_val)
  {
    case 'F':  //the command to go front
      Car_front();
      break;
    case 'B':  //the command to go back
      Car_back();
      break;
    case 'L':  //the command to turn left
      Car_left();
      break;
    case 'R':  //the command to turn right
      Car_right();
      break;
    case 'S':  //the command to stop
      Car_Stop();
      break;
  }
}

/***************The function to run the motor***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  //Go back
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  //show the image to go front
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  //show the image to turn lefr
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  //show the image to turn right
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  //show the image to stop
}

//This function is used for dot matrix screen display
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  //Function to call data transfer start condition
  IIC_send(0xc0);  //Choose an address
  for (int i = 0; i < 16; i++) //Pattern data has 16 bytes
  {
    IIC_send(matrix_value[i]); //transfer pattern data
  }
  IIC_end();   //End pattern data transfer
  IIC_start();
  IIC_send(0x8A);  //display control, select pulse width as 4/16
  IIC_end();
}

//Conditions for the start of data transfer
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

//the sign of ending data transmission
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

//transfer data
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) //each character has 8 digits, which is detected one by one
  {
    if (send_data & mask)  //set high or low levels in light of each bit(0 or 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); //Pull the clock pin SCL_Pin high to stop data transmission
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); //pull down the clock pin SCL_Pin to change signals of SDA
  }
}
```

#### **(6)Test Result:**

After uploading the code, connect the robot to the Bluetooth module and pair the Bluetooth APP. Turn on the powerswitch of the motor drive shield. Place the robot on the floor, you can use these buttons of the Bluetooth app to control the robot. 

![](media/4655aeffe0d2081fa2b9fd254113c392.jpeg)

1. The up, down, left and right arrows control the robot to move forward, backward, left and right respectively.


![](./media/img-20240117095345.png)

2. Click the joystick button and pull the direction of the black point in the white circle to control the movement direction of the robot.

![](./media/img-20240117095401.png)

3.Click the Gravity button and tilt the phone in the forward, backward, left, and right directions, and the robot will move in the direction in which the phone istilted.

![](./media/img-20240117095419.png)
