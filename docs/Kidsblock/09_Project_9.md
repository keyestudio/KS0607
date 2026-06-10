### Project 9: 8*16 Facial Expression LED Dot Matrix

#### **(1)Description:**

Won’t it be fun if a expression board is added to the robot? And the Keyestudio 8*16 LED dot matrix can do the trick. With the help of it, you could design facial expressions, images, patterns and other displays by yourselves.

The 8*16 LED board comes with 128 LEDs. The data of the microprocessor (Arduino) communicates with the AiP1640 through a two-wire bus interface. Therefore, it can control the on and off of 128 LEDs on the module, so as to make the dot matrix on the module to display the pattern you need. A HX-2.54 4Pin cable is provided for your convenience of wiring.

#### **(2)Parameters:**

-   Working voltage: DC 3.3-5V

-   Power loss: 400mW

-   Oscillation frequency: 450KHz

-   Drive current: 200mA

-   Working temperature: -40\~80℃

-   Communication mode: two-wire bus

#### **(3)Knowledge:**

**Circuit of the 8\*16 LED dot matrix**

![](media/edf6c77d05904eebbaa89d557e9e9c1a.png)

**Principle of the 8\*16 LED dot matrix**

How to control each LED of the 8\*16 dot matrix? It is known that each byte has 8 bits and each bit is 0 or 1. when it is 0, LED is off while when it is 1 LED is on. One byte can control one column of the LED,and naturally 16 bytes can control 16 columns of LEDs, that’s the 8\*16 dot matrix.

**Pins description and communication protocol**

The data of the microprocessor (Arduino) communicates with the AiP1640 through a two-wire bus cable.

The communication protocol diagram is as follows (SCLK) is SCL, (DIN) is SDA.

![](media/ea2bab37f23c09453c680590b84653d6.png)

①The starting condition for data input: SCL is high level and SDA changes from high to low.

②For data command setting, there are methods as shown in the figure below.

In our sample program, select the way to **add 1 to the address automatically**, the binary value is 0100 0000 and the corresponding hexadecimal value is 0x40.

![](media/image-20230907161100692.png)

③For address command setting, the address can be selected as shown below.

The first 00H is selected in our sample program, and the binary number 1100 0000 corresponds to the hexadecimal 0xc0.

![](media/image-20230907161152467.png)


④The requirement for data input is that when SCL is at high level when inputting data, the signal on SDA must remain unchanged. Only when the clock signal on SCL is at low level, can the signal on SDA be changed. The input of data is the low bit first, and the high bit later.

⑤The condition for the end of data transmission is that when SCL is at low level, SDA at low level and SCL at high level, the level of SDA becomes high.

⑥Display control, set different pulse width, pulse width can be selected as shown in the figure below.

In the example, the pulse width is 4/16, and the hexadecimal corresponding to 1000 1010 is 0x8A.

![](media/image-20230907161220995.png)

**Instructions for the use of modulus tool**

The dot matrix tool uses the online version, and the link is: <http://dotmatrixtool.com/#>

①Enter the link and the page appears as shown below

![](media/354693b5679a2615c62e99b7025d6355.png)

②The dot matrix is 8\*16, so adjust the height to 8 and width to 16, as shown in the figure below.

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Generate hexadecimal data from the pattern.

As shown in the figure below, press the left mouse button to select, right click to cancel; draw the pattern you want, click Generate, and the hexadecimal data we need will be generated.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)Connection Diagram:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

The GND, VCC, SDA, and SCL of the 8x16 LED light board are respectively connected to the G(GND), V (VCC), A4 and A5 of the expansion board for two-wire serial communication.

(<span style="color: rgb(255, 76, 65);">Note:</span> though it is connected with the IIC pin of Arduino, this module is not for IIC communication. And the IO port here is to simulate I2C communication and can be connected with any two pins )

#### **(5)Test Code:**


You can also drag blocks to edit your code, as shown below

![](media/e346413e7f38f5f6368dd8262f173514.png)

![](media/8ecfff600093779602b37d2202493057.png)

![](media/0f0df06e3ed2adbbe3ffaa20dd3fa0a5.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/75e6f65c9a299868d37544ac42c54f66.png)

#### **(6)Test Results:**

After uploading the test code successfully, wire up, turn the DIP switch to the ON end and power up, a smile-shaped pattern shows on the dot matrix.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)Extension Practice:**

We use the modulus tool we just learned, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), to make the dot matrix display the pattern start , go forward, and stop and then clear the pattern. The time interval is 2000 ms.

![](media/31ab1346c58438ca95c990e4ff963c0d.png)

Block to show smile face![](media/1702a82ce685e3e7da7b136cbc51e718.png)

Code to show expression![](media/bae6801afc8fbcc0e7a70c243559c266.png)

Block to show heart![](media/dcaa414f16d10068d2c3627959141da6.png)

Code for moving forward![](media/8fc218e6b35826aa31f5e00f61414651.png)

Block for going back![](media/043abae4540c578f93772ed9b6648e60.png)

Block for turning left![](media/7b3d80a76228ee5b23555af17269a02d.png)

Block for turning right![](media/5a84b3538a62367a8f35cc59071c0bda.png)

Block for stopping![](media/733bd1f96e1c9d116033a317cb507fac.png)

Block for clearing up![](media/06d37680acd61c9c5c4113c78c985eca.png)

You can also drag blocks to edit your code, as shown below.

（1）![](media/e346413e7f38f5f6368dd8262f173514.png)

（2）![](media/840217b5879f1fce9e36566dc76914a4.png)

（3）![](media/e72e75122897b0ef930196f762080623.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/dee30ed46775feb634d4e8e4ec0a189a.png)

Upload the code to the development board, the 8\*16 board will show following patters.

![](./media/image-20250709134319784.png)

![](./media/image-20250709134332835.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)
