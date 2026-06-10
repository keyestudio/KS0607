### Project 16: Bluetooth Remote Control

![](./media/img-20240111140012.png)

#### **(1)Description:**

In the last several decades, Bluetooth has become the most popular wireless communication module for it is easy to use and has found wide applications in most devices powered by batteries.

In order to adjust with the time and reality and need the needs of customers, Bluetooth has been upgraded several times. In recent years, it embraces lots of transformations in terms of data transfer rate, power consumption of wearable devices and IoT devices, and security systems and others. Here, we plan to learn about DX-BT24 with Arduino board.

#### **(2)Parameter:**

- Bluetooth Protocol: Bluetooth Specification V5.1 BLE

- Serial port sending and receiving without byte limit

- Communication distance: 40m (open environment)

- Operating frequency: 2.4GHz ISM band

- Modulation method: GFSK (Gaussian Frequency Shift Keying)

- Security Features: Authentication and Encryption

- Support Services: Central and Peripheral UUIDs FFE0, FFE1, FFE2

- Power consumption: automatic sleep mode, standby current 400uA\~800uA, 8.5mA during transmission.
  
- Power supply: 5V

- Operating temperature: –10 to +65 degrees Celsius

#### **(3)Connection Diagram:**

1.STATE is the status test pin connected to the internal light-emitting diode and usually remains unconnected.

2.RXD is the serial port interface for receiving terminal.

3.TXD is the serial port interface for sending terminal.

4.GND is for ground.

5.VCC is the positive pole.

6.EN/BRK: the disconnection of it represents the disconnection of the Bluetooth and it usually remains unconnected.

(Note: here the Bluetooth is directly linked with the V2 shield and **please pay attention to the direction**)

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)


#### **(4)Download and install APP:**

##### **For IOS system**

1\. Open App Store.

2\. Search <span style="color: rgb(61, 167, 66);">KeyesRobot</span> in the Apple Store and click download.

![](./media/img-20240111141301.png)

3\. After the app is installed, you will see the following icon on your phone desktop.

![](./media/img-20240111141412.png)

**How to connect iOS Phone to Bluetooth module:**

1\. Turn on the Bluetooth and location services on phone through settings.

![](./media/img-20240111141943.png)

2\. Allow KeyesRobot APP to access Bluetooth through settings.

![](./media/img-20240111142052.png)

3\. Click to open KeyesRobot App.

![](./media/img-20240111142140.png)

4\. KeyesRobot App is a universal APP, which is applied to multiple keyestudio robots. If the interface does not display "TANK ROBOT", you can click the left and right buttons to find "TANK ROBOT".

5\. Click the <span style="color: rgb(61, 167, 66);">Bluetooth </span>button ![](./media/img-20240111142336.png) in the upper right corner to scan the bluetooth

![](./media/img-20240111142415.png)

6\. You will see a Bluetooth named <span style="color: rgb(0, 209, 0);">**BT24**</span>, click the <span style="color: rgb(255, 169, 0);">Connect</span> button.

![](./media/img-20240111142536.png)

7\. If the onboard LED on the Bluetooth module stops flashing and stays on, it means your phone is successfully connected to the Bluetooth module.

![](./media/img-20240111142702.png)


##### **For Android System**

1\. Search <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> in Google Play, or open the following link to download and install the app. 

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Turn on the Bluetooth and the location services of the mobile phone

![](./media/img-20240111143354.png)

3\. Find the KeyesRobot Bluetooth app from settings, click on the permission options of the app, and
enable Location and nearby device permissions.(<span style="color: rgb(255, 76, 65);">Note:</span> Some mobile phones do not have nearby device permissions function.)

![](./media/img-20240111143451.png)

4\. Click to open KeyesRobot App.

![](./media/img-20240111143529.png)

5\. KeyesRobot App is a universal APP, which is applied to multiple keyestudio robots. If the interface does not display "TANK ROBOT", you can click the left and right buttons to find "TANK ROBOT".

6\. Click the <span style="color: rgb(61, 167, 66);">Bluetooth </span> button ![](./media/img-20240111142336.png) in the upper right corner to scan the bluetooth

![](./media/img-20240111142415.png)

7\. You will see a Bluetooth named <span style="color: rgb(0, 209, 0);">**BT24**</span>, click the <span style="color: rgb(255, 169, 0);">Connect</span> button.

![](./media/img-20240111143910.png)

8\. When your phone is successfully connected to the Bluetooth module, the onboard LED on the Bluetooth module will stop flashing and stay on.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(5)Test the Bluetooth APP:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.1
Bluetooth
http://www.keyestudio.com
*/

char ble_val; //Character variable(used to store the value received by Bluetooth)

void setup() 
{
	Serial.begin(9600);
}

void loop() 
{
    if (Serial.available() > 0) //Determine whether there is data in the serial port buffer
    {
        ble_val = Serial.read(); //Read the data in the serial port buffer
        Serial.println(ble_val); //Print out
    }
}
```

Upload the code to the development board, then plug in the Bluetooth module, and then connected the mobile phone to the Bluetooth module.

After the mobile phone is successfully connected to the Bluetooth module, click to open the Bluetooth APP and click the <span style="color: rgb(0, 252, 255);">Select</span> button on the <span style="color: rgb(0, 252, 255);">homepage</span>.

![](./media/img-20240111144744.png)

The main interface of the Bluetooth app is shown in the figure below.

![](./media/img-20240111144859.png)

After the code above is successfully uploaded, open the serial monitor of the arduino IDE and set the baud rate to 9600. Click the icon on the APP interface and the serial monitor will display command sent by button.

![](media/805f8ee5c8998a5d6cb8bcef9da09186.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Note: The APP connection method is the same as below.**</span>
<br>
<b>

#### **(6)Code Explanation:**

**Serial.available()** represents the number of characters currently remaining in the serial port buffer. 

This function is generally used to determine whether there is data in this area. When Serial.available()\>0, it means that the serial port has received data and can be read.

**Serial.read()** refers to taking out and reading a Byte of data from the serial port buffer. For example, if a device sends data to the Arduino through the serial port, we can use Serial.read() to read the sent data.

#### **(7)Expansion Project:**

Here we use the command sent by the mobile phone to turn on or off an LED light. Looking at the wiring diagram, an LED is connected to the D9 pin.

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)

**Test Code**

(<span style="color: rgb(255, 76, 65);">Note: </span> Do not connect the Bluetooth module before uploading the code, because the uploading of the code also uses serial communication, and there may be conflicts with the serial communication of the Bluetooth, which can cause the uploading of the code to fail.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.2
Bluetooth
http://www.keyestudio.com
*/

int LED = 9;
char ble_val; //Integer variable used to store the value received by Bluetooth

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);
}

void loop() 
{

    if (Serial.available() > 0) //Determine whether there is data in the serial port buffer
    {
        ble_val = Serial.read(); //Read data from serial port buffer
        Serial.print("DATA RECEIVED:");
        Serial.println(ble_val);
        if (ble_val == 'a') 
        {
            digitalWrite(LED, HIGH);
            Serial.println("led on");
        }
        if (ble_val == 'b') 
        {
            digitalWrite(LED, LOW);
            Serial.println("led off");
        }
    }
}
```

![](media/3577f17c526b1dc55d4f587ef95f2d08.png)

After the code above is successfully uploaded, open the serial monitor of the arduino IDE and set the baud rate to 9600. Click ![](media/3fd6c998c0f665fb607a5827794b9bfe.png) to control the LED. When clicking it, a character a will be sent, then LED will be on. If this button is pressed again, the LED will be off.

![](./media/img-20240117094533.png)

![](media/b45c3c46391467218fe07003dbb2f3e3.png)

You need to remove the BT module if you finish projects.
