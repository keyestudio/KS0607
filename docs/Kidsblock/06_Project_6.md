### Project 6: Ultrasonic Sensor

#### **(1)Description:**

![](media/0180b169a1c3b228394b43df704fac32.png)

The HC-SR04 ultrasonic sensor uses sonar to determine distance to an object like what bats do. It offers excellent non-contact range detection with high accuracy and stable readings in an easy-to-use package. It comes complete with ultrasonic transmitter and receiver modules.

The HC-SR04 or the ultrasonic sensor is being used in a wide range of electronics projects for creating obstacle detection and distance measuring application as well as various other applications. Here we have brought the simple method to measure the distance with Arduino and ultrasonic sensor and how to use ultrasonic sensor with Arduino.

![](./media/image-20250709133626194.png)

#### **(2)Parameters:**

- Power Supply :+5V DC

- Quiescent Current : \<2mA

- Working Current: 15mA

- Effectual Angle: \<15°

- Ranging Distance : 2cm – 400 cm

- Resolution : 0.3 cm

- Measuring Angle: 30 degree

- Trigger Input Pulse width: 10uS

#### **(3)The principle of ultrasonic sensor:**

As the above picture shown, it is like two eyes. One is transmitting end, the other is receiving end.

The ultrasonic module will emit the ultrasonic waves after triggering a signal. When the ultrasonic waves encounter the object and are reflected back, the module outputs an echo signal, so it can determine the distance of the object from the time difference between the trigger signal and echo signal. 

Here, t is the time from when the emitted signal meets the obstacle to when it returns. The propagation speed of sound in the air is about 343m/s, and distance = speed * time. However, since the ultrasonic wave travels to the obstacle and back, the time represents twice the distance. Therefore, it needs to be divided by 2. The distance measured by the **ultrasonic wave = (speed * time) / 2**.

1. Use method and timing chart of ultrasonic module:

2. Setting the delay time of Trig pin of SR04 to 10μs at least, which can trigger it to detect distance.

3. After triggering, the module will automatically send eight 40KHz ultrasonic pulses and detect whether there is a signal return. This step will be completed automatically by the module.

4. If the signal returns, the Echo pin will output a high level, and the duration of the high level is the time from the transmission of the ultrasonic wave to the return.

![](media/image-20230525110337646.png)

Circuit diagram of ultrasonic sensor:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4)Connection Diagram:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Wiring Note:</span> The VCC pin of the ultrasonic sensor module is connected to the 5v(V) of the Keyestudio 8833 motor drive expansion board, the Trig pin is connected to digital D12, the Echo pin is connected to digital D13, and the Gnd pin is connected to Gnd(G);

#### **(5)Test Code:**

You can also drag blocks to edit your code, as shown below.

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/128e0b4ee7d3448410d72312175bc6da.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/a6df8829b69f7faed26a73d01da8d50d.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/eca0805413af12957d319c706d3e7cdb.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/569aff5ff2cbd2f3605f217ebb5ed50b.png)

#### **(6)Test Results:**

Upload the test code to the development board, open the serial monitor, and set the baud rate to 9600. The detected distance will be displayed in cm and inches. When you hinder the ultrasonic sensor with your hand, the displayed distance value will get smaller.

![](media/4f77acbf5b226e20e3cdd70c0f90602e.png)

#### **(7)Extension Practice:**

We have just measured the distance displayed by the ultrasonic. How about controlling the LED with the measured distance? Let's try it and connect an LED light module to the D9 pin.

![](media/291ac1db0f38418772d11bb1786b7314.png)


You can also drag blocks to edit your code, as shown below

![](media/8de1b04be1ba147dd242c66bddeacacc.png)

![](media/49d5523ae565e1d4dfc3504d1e1748d4.png)

![](media/413019f6b04d6d904a438ac6c8589d64.png)

![](media/8d5fc923f5ded5305f36b1379c1ba38e.png)

![](media/25bf5c6f26cce9db18dfe951e7f166fe.png)

![](media/a6205e42e005084c33c247fe564bdcad.png)

![](media/b6e575b05bdc050e32c9b2e54e61a750.png)

**Complete Test Code**

(<span style="color: rgb(255, 76, 65);">**Note:**</span> Do not connect the Bluetooth module before uploading the code, because uploading the code also uses serial communication, and there may be conflicts with the Bluetooth serial communication, which can cause the upload to fail.)

![](media/065eac0ad9cfa8f07aeb5e648698bdb5.png)

Upload the test code to the development board, move your hand close to the ultrasonic sensor, and check if the LED turns on.

![](./media/img-20240117092413.png)
