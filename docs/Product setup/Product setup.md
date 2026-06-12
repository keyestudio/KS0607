# 2. Produktinstallation

<span style="color: rgb(255, 76, 65);">**Vorsicht**</span>: Stellen Sie den Anfangswinkel des Servos ein und entfernen Sie Schutzfolien von den Platinen, bevor Sie diesen Roboter installieren.

![](./media/image-20250709092645945.png)

 **Schritt 1**

![KS0607_18](./media/KS0607_18.png)

![KS0607_19](./media/KS0607_19.png)

![KS0607_20](./media/KS0607_20.png)

Bitte zuerst die Kabel anschließen.

![](./media/image-20250709093344681.png)

![KS0607-099](./media/KS0607-099.jpg)

![KS0607_21](./media/KS0607_21.png)

![KS0607_22](./media/KS0607_22.png)

![KS0607_23](./media/KS0607_23.png)

**Schritt 2**

![KS0607_24](./media/KS0607_24.png)

![KS0607_25](./media/KS0607_25.png)

![KS0607_26](./media/KS0607_26.png)

**Schritt 3**

![KS0607_28](media\KS0607_28.png)

![KS0607_29](./media/KS0607_29-177909268352217.png)

![KS0607_30](./media/KS0607_30-177909269696918.png)

 **Schritt 4**

![KS0607_31](./media/KS0607_31-17790915380363.png)

![KS0607_32](./media/KS0607_32-17790915471644.png)

![KS0607_33](./media/KS0607_33-17790915540415.png)

![KS0607_34](./media/KS0607_34-17790915654246.png)

![KS0607_35](./media/KS0607_35-17790915710247.png)



**Schritt 5**

![KS0607_36](./media/KS0607_36-17790915806918.png)

<span style="color: rgb(255, 76, 65);">Achten Sie auf die Richtung der Jumper-Kappen.</span>

![KS0607_37](./media/KS0607_37-17790915896649.png)

![KS0607_38](./media/KS0607_38-177909159600610.png)

 **Schritt 6**

![KS0607_39](./media/KS0607_39.png)

![KS0607_40](./media/KS0607_40.png)

![KS0607_41](./media/KS0607_41.png)

**Schritt 7**

![KS0607_42](./media/KS0607_42.png)

![KS0607_43](./media/KS0607_43.png)

![KS0607_44](./media/KS0607_44.png)

**Schritt 8**

（Der Winkel des Servos muss eingestellt werden）

![KS0607-098](./media/KS0607-098.jpg)

![KS0607-097](./media/KS0607-097.jpg)

**Stellen Sie den Winkel des Servos auf 90° ein**

Um den Code des Servos anzupassen, wählen Sie bitte entsprechend dem Kurs aus.

1.**Arduino:** Laden Sie die Code-Datei herunter: [Arduino](./Arduino.7z)

![](./media/image-20250710110650230.png)

2.**Kidsblock:** Laden Sie die Code-Datei herunter: [Kidsblock](./Kidsblock.7z)

![](./media/image-20250710110906515.png)

**Nach der Initialisierung des Servo-Winkels das Bluetooth-Modul einbauen.**

Halten Sie den Ultraschallsensor parallel zur Platine.

![KS0607-096](./media/KS0607-096.jpg)

![](./media/image-20250709095307371.png)

 **Schritt 9**

![KS0607_48](./media/KS0607_48-177909161769011.png)

![KS0607_49](./media/KS0607_49-177909162425112.png)

![KS0607_50](./media/KS0607_50-177909163131113.png)

**Schritt 10**

![KS0607_51](./media/KS0607_51-177909163803814.png)

![KS0607_52](./media/KS0607_52-177909164311315.png)

![KS0607_53](./media/KS0607_53-177909164907716.png)

**Verkabelung**

Für das 8\*16 LED-Panel die Kabel mit A4 und A5 verbinden.

![](./media/image-20250709095552072.png)

![](./media/image-20250709095606248.png)

![](./media/image-20250709095643567.png)

Motor A an Port A und Motor B an Port B anschließen.

![](./media/image-20250709095728739.png)

![](./media/image-20250709095740866.png)

Das Stromversorgungskabel anschließen.

![](./media/image-20250709095759390.png)

![](./media/image-20250709095811580.png)

Linienverfolgungssensor (siehe Abbildung)

![](./media/image-20250709095830428.png)

![](./media/image-20250709095848550.png)

![](./media/image-20250709095901776.png)

![](./media/image-20250709095911639.png)

Fotowiderstände anschließen

![](./media/image-20250709095929779.png)

![](./media/image-20250709095939414.png)

| Fotowiderstand | Keyestudio 8833 Board |
| :------------: | :-------------------: |
|       G        |           G           |
|       V        |           V           |
|       s        |          A1           |

![](./media/image-20250709100043670.png)

| Fotowiderstand | Keyestudio 8833 Board |
| :------------: | :-------------------: |
|       G        |           G           |
|       V        |           V           |
|       S        |          V2           |

Ultraschallsensor anschließen.

![](./media/image-20250709100317508.png)

![](./media/image-20250709100329430.png)

| Ultraschallsensor | Keyestudio 8833 Board |
| :---------------: | :-------------------: |
|        Vcc        |           V           |
|       Trig        |          D12          |
|       Echo        |          D13          |
|        Gnd        |           G           |

Servo anschließen (D10)

![](./media/image-20250709100626238.png)

| Servo  | Keyestudio 8833 Board |
| :----: | :-------------------: |
| Braun  |           G           |
|  Rot   |         V(5V)         |
| Orange |          D10          |

<span style="color: rgb(255, 76, 65);">**Wir verwenden einen 18650-Lithium-Akku mit einem spitzen Pluspol, dessen Leistung und Kapazität keine besonderen Anforderungen haben.**</span>

![](./media/image-20250709100841625.png)