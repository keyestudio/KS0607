### Project 18: Ultrasonic Tank Robot Multiple Functions

#### **(1)Description:**

The smart car has performed a single function in every previous project.

Can it display multiple functions at a time? Yes, it can.

In this final large project, we intend to use a complete code to control the smart car to demonstrate all the functions mentioned in the previous projects. We use the keys on the Bluetooth APP to automatically switch between various functions, which is quite simple and convenient.

#### **(2)Flow Diagram:**

![](media/wps122.png)

#### **(3)Connection Diagram:**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA, and SCL of the 8x16 board are connected to G (GND), + (VCC), A4, and A5 of the expansion board.

2\. VCC, Trig, Echo, and Gnd of the ultrasonic sensor are connected to 5V (V), 12 (S), 13 (S), and Gnd (G).

3\. The brown wire, red wire, and orange wire of the servo are connected to Gnd (G), 5v (V), and D10.

4\. RXD, TXD, GND, and VCC of the BT module are connected to TX, RX, G (GND), and 5V (VCC). STATE and BRK don’t need to be interfaced.

5\. The pins "G", "V", and S of the left photoresistor module are connected to G (GND), V (VCC), and A1, respectively; The right photoresistor module is connected to G (GND), V (VCC), and A2, respectively.

6\. The distal ports of the line tracking sensor are 11, 7, and 8.

#### **(4)Test Code:**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

<span style="color: rgb(255, 76, 65);">**Note:**</span> You can’t speed up the car via the App.

![](media/e3c4c6cf504b1b9ea6fbae63f5fd9077.png)

#### **(5)Test Result:**

Before uploading the program code, the Bluetooth module needs to be removed; otherwise, the code upload will fail.

After uploading the code successfully, turn on location services on your device, and then connect the Bluetooth module.

Once the Bluetooth module is plugged in and powered on, and the mobile APP is successfully connected to the Bluetooth, we can use the mobile APP to control the tank robot.
