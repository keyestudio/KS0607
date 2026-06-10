### Project 16: Bluetooth Remote Control

![](./media/image-20250709134858245.png)

#### **(1)Description:**

In the last several decades, Bluetooth has become the most popular wireless communication module for it is easy to use and has found wide applications in most devices powered by batteries.

In order to adjust with the time and reality and need the needs of customers, Bluetooth has been upgraded several times. In recent years, it embraces lots of transformations in terms of data transfer rate, power consumption of wearable devices and IoT devices, and security systems and others. Here, we plan to learn about DX-BT24 with Arduino board.

#### **(2)Parameter:**

- Bluetooth protocol: Bluetooth Specification V5.1 BLE
- Working distance: In an open environment, achieve 40m ultra-long distance
- Communication Operating frequency: 2.4GHz ISM band
- Communication interface: UART
- Bluetooth certification: in line with FCC CE ROHS REACH certification standards
- Serial port parameters: 9600, 8 data bits, 1 stop bit, invalid bit, no flow control
- Power: 5V DC
- Operating temperature: –10 to +65 degrees Celsius


#### **(3)Application:**

The DX-BT24 module also supports the BT5.1 BLE protocol, which can be directly connected to iOS devices with BLE Bluetooth function, and supports resident running of background programs. Mainly used in the field of short-distance wireless data transmission. Avoid cumbersome cable connections and can directly replace serial cables. Successful application areas of BT24 modules:

※ Bluetooth wireless data transmission; 

※ Mobile phone, computer peripheral equipment; 

※ Handheld POS equipment; 

※ Wireless data transmission of medical equipment;

※ Smart home control; 

※ Bluetooth printer; 

※ Bluetooth remote control toys; 

※ Shared bicycles;

#### **(4)Pins description:**

![](media/cd97cf79ff5cdd5bbd78f4cc960d38e5.png)

①STATE：state pin

②RX：reception pin

③TX：sending pin

④GND：grounded

⑤VCC：power pin

⑥EN：enable pin

Connect Bluetooth to the development board

| Uno  | BT24 |
| :--: | :--: |
|  TX  |  RX  |
|  RX  |  TX  |
| VCC  |  5V  |
| GND  | GND  |

#### **(5)Connection Diagram:**

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)

#### **(6)Download APP:**

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

5\. Click the <span style="color: rgb(61, 167, 66);">Bluetooth button</span>![](./media/img-20240111142336.png) in the upper right corner to scan the bluetooth

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

6\. Click the <span style="color: rgb(61, 167, 66);">Bluetooth button</span>![](./media/img-20240111142336.png) in the upper right corner to scan the bluetooth

![](./media/img-20240111142415.png)

7\. You will see a Bluetooth named <span style="color: rgb(0, 209, 0);">**BT24**</span>, click the <span style="color: rgb(255, 169, 0);">Connect</span> button.![](./media/img-20240111143910.png)

8\. When your phone is successfully connected to the Bluetooth module, the onboard LED on the Bluetooth module will stop flashing and stay on.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(7)BT Test Code:**

You can also drag blocks to edit your code, as shown below

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/19a90ffb7565966f7d40462abed876a7.png)

（5）![](media/c8228c5040a43ae322612b312c995ac3.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/4766ada3bf48bb35522f292d9352bb78.png)


Upload the code to the development board, then plug in the Bluetooth module, and then connected the mobile phone to the Bluetooth module.

After the mobile phone is successfully connected to the Bluetooth module, click to open the Bluetooth APP and click the <span style="color: rgb(0, 252, 255);">Select</span> button on the <span style="color: rgb(0, 252, 255);">homepage</span>.

![](./media/img-20240111144744.png)

The main interface of the Bluetooth app is shown in the figure below.

![](./media/img-20240111144859.png)

Click ![Img](./media/img-20240111171312.png)and set the baud rate to 9600. Click the icon on the APP interface and the serial monitor will display command sent by button.

![](media/f5004f5334fb4885ac0096f99e4133f9.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Note: The APP connection method is the same as below.**</span>
<br>
<br>


#### **(8)Extension Practice:**

In the above project, Bluetooth receives the signal sent by the mobile phone and displays it on the serial port of the development board. Here we use the command sent by the mobile phone to turn on or off an LED. Looking at the wiring diagram, an LED is connected to the D9 pin,

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)


You can also drag blocks to edit your code, as shown below

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/aa78663af261ff1d9bc8ffa6ad7a65bc.png)

(5）![](media/c8228c5040a43ae322612b312c995ac3.png)

（6）![](media/4164bcf66d3d2415f43a0efcd1ce4243.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/91fd9d6f85e291fe90a63e5095ed7f44.png)

After the code above is successfully uploaded. Click ![](media/d5e59839bafc63f8b35c78c60573d1fc.png) to control the LED.

![](./media/img-20240117094418.png)


After you finish the BT project, remove it.
