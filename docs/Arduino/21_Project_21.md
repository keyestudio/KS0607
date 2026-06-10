### Project 21: Fan

#### **(1)Description：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

This fan module uses a HR1124S motor-controlling chip, a single-channel H-bridge driver chip containing a low-conductivity resistance PMOS and NMOS power tubes. The low-conducting resistance can ease the power consumption, contributing to the safe work of the chip for longer time. 

In addition, its low standby current and low static working current makes itself apply to toys. We can control the rotation direction and speed of the fan by outputting IN + and IN- signals and PWM signals.

#### **(2)Specification:**

Working voltage: 5V

Current: 200MA

Maximum power: 2W

Operating temperature: -10 degrees Celsius to +50 degrees Celsius

Size: 47.6MM \*23.8MM

#### **(3)Connection Diagram:**

The fan module needs driving by large current; therefore, we install a battery holder.

![](media/2bd9aa5cc21e274458328958561f1915.png)

The pin GND, VCC, IN+ and IN- of the fan module are connected to pin G, V, D12 and D13 of the shield.

#### **(4)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.1
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;

void setup()
{
    pinMode(INA, OUTPUT);//Set digital port INA as output
    pinMode(INB, OUTPUT);//Set digital port INB as output
}

void loop() 
{
    //Set the fan to rotate anticlockwise for 3s
    digitalWrite(INA, LOW);
    digitalWrite(INB, HIGH);
    delay(3000);
    //Set the fan to stop for 1s
    digitalWrite(INA, LOW);
    digitalWrite(INB, LOW);
    delay(1000);
    //Set the fan to rotate clockwise for 3s
    digitalWrite(INA, HIGH);
    digitalWrite(INB, LOW);
    delay(3000);
}
```

#### **(5)Test Results：**

Upload code, wire up components and plug in power. The small fan will turn anticlockwise for 3000ms, stop for 1000ms, and clockwise for 300ms.

![](./media/img-20240117085032.png)

#### **(6)Extension Practice:**

We have understood the working principle of the flame sensor. Next, hook up a flame sensor in the circuit , as shown below. Then control the fan to blew out fire with the flame sensor.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 21.2
130 motor
http://www.keyestudio.com
*/

int INA = 12;
int INB = 13;
int flame = A1; //Define the flame pin as analog pin A1
int val = 0; //Define digital variables

void setup() 
{
    pinMode(INA, OUTPUT);//Set digital port INA as output
    pinMode(INB, OUTPUT);//Set digital port INB as output
    pinMode(flame, INPUT); //Define the flame as an input source
}

void loop() 
{
    val = analogRead(flame); //Read the analog value of the flame sensor
    if (val <= 700)  //When analog value≤700, fan is on
    {
        //Turn on the fan when flame is detected
        digitalWrite(INA, LOW);
        digitalWrite(INB, HIGH);
    } 
    else 
    {
        //Otherwise it stops operating
        digitalWrite(INA, LOW);
        digitalWrite(INB, LOW);
    }
}
```

After uploading the code, turn on the power switch of the motor drive shield, you can turn on the fan when flame is detected from the left flame sensor of the robot.

![](./media/image-20250709115926832.png)
