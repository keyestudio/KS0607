### Project 3: Photoresistor

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Description:**

The photosensitive resistor is a special resistor made of a semiconductor material such as a sulfide or selenium, and a moisture-proof resin is also coated with a photoconductive effect. The photosensitive resistance is most sensitive to the ambient light, different illumination strength, and the resistance of the photosensitive resistance is different. We use the photosensitive resistance to design the photosensitive resistor module. 

The module signal is connected to the microcontroller analog port. When the light intensity is stronger, the larger the analog port voltage, that is, the simulation value of the microcontroller is also large; in turn, when the light intensity is weaker, the smaller the analog port voltage, that is, the simulation value of the microcontroller is also small. 

In this way, we can read the corresponding analog value using the photosensitive resistor module, and the intensity of the light in the inductive environment.

![](./media/image-20250709122809574.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parameters:**

- Photosensitive resistance resistance value: 5K Ou-0.5m

- Interface type: simulation port A0, A1

- Working voltage: 3.3V-5V

- Pin spacing: 2.54mm

#### **(3)Connection Diagram:**

What we are going to test next isthe photoresistor module on the leftside ofthe robot.

![](./media/img-20240117091730.png)

The left photoresistoris connected to A1/P3 of the motor drive shield.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)


#### **(4)Test Code:**

You can also drag blocks to edit your code, as shown below.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/f29c7da2238bcc2bc70cb4b2c773b50d.png)

#### **(5)Test Results:**

Upload the code to the development board. Click ![](media/9011f20d83897d7a5936793c4ae142fc.png) to set baud rate 9600.When covering it with your hand, the value gets smaller; if not, the value gets larger.

![](media/53e2fc37ee5bb2c6ec187c309c431c47.png)



#### **(6)Extension Practice:**

The above code just reads the value of the photoresistor. We can make the photosensitive and LED combine to change the LED.How about controlling the LED’s brightness by it?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

PWM can change the light brightness, that is, LED should be connected to the PWM of the development board.

Connect the LED to D9 and keep other pins unchanged, then we edit code.

You can also drag blocks to edit your code, as shown below.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/b94c3789429c5fed4fd38467cb9792dd.png)

![](media/9ecdfd77e2a69dea5a8df04e7d56a13a.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/b23bcae806e8e27382b162909d30f3c0.png)

Upload the code to the development board, we press the photoresistor to see if the brightness of the LED light has changed.

![](./media/img-20240117091759.png)
