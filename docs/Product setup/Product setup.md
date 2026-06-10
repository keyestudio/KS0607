# 2. Product Installation

<span style="color: rgb(255, 76, 65);">**Caution**</span>: Set the initial angle of the servo Peel thin films off boards before installing this robot .

![](./media/image-20250709092645945.png)

 **Step1**

![KS0607_18](./media/KS0607_18.png)

![KS0607_19](./media/KS0607_19.png)

![KS0607_20](./media/KS0607_20.png)

Please wire up first.

![](./media/image-20250709093344681.png)

![KS0607-099](./media/KS0607-099.jpg)

![KS0607_21](./media/KS0607_21.png)

![KS0607_22](./media/KS0607_22.png)

![KS0607_23](./media/KS0607_23.png)

**Step2 **

![KS0607_24](./media/KS0607_24.png)

![KS0607_25](./media/KS0607_25.png)

![KS0607_26](./media/KS0607_26.png)

**Step 3**

![KS0607_28](media\KS0607_28.png)

![KS0607_29](./media/KS0607_29-177909268352217.png)

![KS0607_30](./media/KS0607_30-177909269696918.png)

 **Step 4**

![KS0607_31](./media/KS0607_31-17790915380363.png)

![KS0607_32](./media/KS0607_32-17790915471644.png)

![KS0607_33](./media/KS0607_33-17790915540415.png)

![KS0607_34](./media/KS0607_34-17790915654246.png)

![KS0607_35](./media/KS0607_35-17790915710247.png)



**Step 5**

![KS0607_36](./media/KS0607_36-17790915806918.png)

<span style="color: rgb(255, 76, 65);">Note the direction of jumper caps.</span>

![KS0607_37](./media/KS0607_37-17790915896649.png)

![KS0607_38](./media/KS0607_38-177909159600610.png)

 **Step 6**

![KS0607_39](./media/KS0607_39.png)

![KS0607_40](./media/KS0607_40.png)

![KS0607_41](./media/KS0607_41.png)

**Step 7**

![KS0607_42](./media/KS0607_42.png)

![KS0607_43](./media/KS0607_43.png)

![KS0607_44](./media/KS0607_44.png)

**Step 8**

（Need to adjust the angle of the servo）

![KS0607-098](./media/KS0607-098.jpg)

![KS0607-097](./media/KS0607-097.jpg)

**Set the angle of the servo to 90°**

To adjust the code of the servo,please select it according to the course.

1.**Arduino:** Download the code file: [Arduino](./Arduino.7z)

![](./media/image-20250710110650230.png)

2.**Kidsblock: **Download the code file: [Kidsblock](./Kidsblock.7z)

![](./media/image-20250710110906515.png)

**After initializing servo angle, install the Bluetooth module.**

Keep the ultrasonic sensor parallel to the board.

![KS0607-096](./media/KS0607-096.jpg)

![](./media/image-20250709095307371.png)

 **Step 9**

![KS0607_48](./media/KS0607_48-177909161769011.png)

![KS0607_49](./media/KS0607_49-177909162425112.png)

![KS0607_50](./media/KS0607_50-177909163131113.png)

**Step 10**

![KS0607_51](./media/KS0607_51-177909163803814.png)

![KS0607_52](./media/KS0607_52-177909164311315.png)

![KS0607_53](./media/KS0607_53-177909164907716.png)

**Wire up**

For 8\*16 LED panel, Make wires connect to A4 and A5.

![](./media/image-20250709095552072.png)

![](./media/image-20250709095606248.png)

![](./media/image-20250709095643567.png)

Connect the motor A to A port and make the motor B to B port.

![](./media/image-20250709095728739.png)

![](./media/image-20250709095740866.png)

Connect the power wire.

![](./media/image-20250709095759390.png)

![](./media/image-20250709095811580.png)

Line Tracking Sensor(see the picture)

![](./media/image-20250709095830428.png)

![](./media/image-20250709095848550.png)

![](./media/image-20250709095901776.png)

![](./media/image-20250709095911639.png)

Wire up the photoresistors

![](./media/image-20250709095929779.png)

![](./media/image-20250709095939414.png)

| Photoresistor | Keyestudio 8833 Board |
| :-----------: | :-------------------: |
|       G       |           G           |
|       V       |           V           |
|       s       |          A1           |

![](./media/image-20250709100043670.png)

| Photoresistor | Keyestudio 8833  Board |
| :-----------: | :--------------------: |
|       G       |           G            |
|       V       |           V            |
|       S       |           V2           |

Wire up ultrasonic sensor.

![](./media/image-20250709100317508.png)

![](./media/image-20250709100329430.png)

| Ultrasonic Sensor | Keyestudio 8833 Board |
| :---------------: | :-------------------: |
|        Vcc        |           V           |
|       Trig        |          D12          |
|       Echo        |          D13          |
|        Gnd        |           G           |

Wire up the servo(D10)

![](./media/image-20250709100626238.png)

| Servo  | Keyestudio 8833 Board |
| :----: | :-------------------: |
| Brown  |           G           |
|  Red   |         V(5V)         |
| Orange |          D10          |

<span style="color: rgb(255, 76, 65);">**We adopt a model 18650 lithium battery with a pointed positive pole, whose power and capacity are not required.**</span>

![](./media/image-20250709100841625.png)

