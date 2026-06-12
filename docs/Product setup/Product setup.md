# 2. Productinstallatie

<span style="color: rgb(255, 76, 65);">**Waarschuwing**</span>: Stel de beginhoek van de servo in en verwijder dunne folies van de platen voordat u deze robot installeert.

![](./media/image-20250709092645945.png)

 **Stap 1**

![KS0607_18](./media/KS0607_18.png)

![KS0607_19](./media/KS0607_19.png)

![KS0607_20](./media/KS0607_20.png)

Sluit eerst de bedrading aan.

![](./media/image-20250709093344681.png)

![KS0607-099](./media/KS0607-099.jpg)

![KS0607_21](./media/KS0607_21.png)

![KS0607_22](./media/KS0607_22.png)

![KS0607_23](./media/KS0607_23.png)

**Stap 2**

![KS0607_24](./media/KS0607_24.png)

![KS0607_25](./media/KS0607_25.png)

![KS0607_26](./media/KS0607_26.png)

**Stap 3**

![KS0607_28](media\KS0607_28.png)

![KS0607_29](./media/KS0607_29-177909268352217.png)

![KS0607_30](./media/KS0607_30-177909269696918.png)

 **Stap 4**

![KS0607_31](./media/KS0607_31-17790915380363.png)

![KS0607_32](./media/KS0607_32-17790915471644.png)

![KS0607_33](./media/KS0607_33-17790915540415.png)

![KS0607_34](./media/KS0607_34-17790915654246.png)

![KS0607_35](./media/KS0607_35-17790915710247.png)



**Stap 5**

![KS0607_36](./media/KS0607_36-17790915806918.png)

<span style="color: rgb(255, 76, 65);">Let op de richting van de jumperkappen.</span>

![KS0607_37](./media/KS0607_37-17790915896649.png)

![KS0607_38](./media/KS0607_38-177909159600610.png)

 **Stap 6**

![KS0607_39](./media/KS0607_39.png)

![KS0607_40](./media/KS0607_40.png)

![KS0607_41](./media/KS0607_41.png)

**Stap 7**

![KS0607_42](./media/KS0607_42.png)

![KS0607_43](./media/KS0607_43.png)

![KS0607_44](./media/KS0607_44.png)

**Stap 8**

（De hoek van de servo moet worden afgesteld）

![KS0607-098](./media/KS0607-098.jpg)

![KS0607-097](./media/KS0607-097.jpg)

**Stel de hoek van de servo in op 90°**

Om de code van de servo aan te passen, selecteer deze op basis van de cursus.

1.**Arduino:** Download het codebestand: [Arduino](./Arduino.7z)

![](./media/image-20250710110650230.png)

2.**Kidsblock:** Download het codebestand: [Kidsblock](./Kidsblock.7z)

![](./media/image-20250710110906515.png)

**Nadat de servo-hoek is geïnitialiseerd, installeert u de Bluetooth-module.**

Houd de ultrasone sensor parallel aan de plaat.

![KS0607-096](./media/KS0607-096.jpg)

![](./media/image-20250709095307371.png)

 **Stap 9**

![KS0607_48](./media/KS0607_48-177909161769011.png)

![KS0607_49](./media/KS0607_49-177909162425112.png)

![KS0607_50](./media/KS0607_50-177909163131113.png)

**Stap 10**

![KS0607_51](./media/KS0607_51-177909163803814.png)

![KS0607_52](./media/KS0607_52-177909164311315.png)

![KS0607_53](./media/KS0607_53-177909164907716.png)

**Bedrading aansluiten**

Voor het 8\*16 LED-paneel, sluit de draden aan op A4 en A5.

![](./media/image-20250709095552072.png)

![](./media/image-20250709095606248.png)

![](./media/image-20250709095643567.png)

Sluit motor A aan op poort A en motor B op poort B.

![](./media/image-20250709095728739.png)

![](./media/image-20250709095740866.png)

Sluit de voedingskabel aan.

![](./media/image-20250709095759390.png)

![](./media/image-20250709095811580.png)

Lijnvolgsensor (zie de afbeelding)

![](./media/image-20250709095830428.png)

![](./media/image-20250709095848550.png)

![](./media/image-20250709095901776.png)

![](./media/image-20250709095911639.png)

Sluit de fotoweerstand aan

![](./media/image-20250709095929779.png)

![](./media/image-20250709095939414.png)

| Fotoweerstand | Keyestudio 8833 Board |
| :-----------: | :-------------------: |
|       G       |           G           |
|       V       |           V           |
|       s       |          A1           |

![](./media/image-20250709100043670.png)

| Fotoweerstand | Keyestudio 8833 Board |
| :-----------: | :-------------------: |
|       G       |           G           |
|       V       |           V           |
|       S       |           V2          |

Sluit de ultrasone sensor aan.

![](./media/image-20250709100317508.png)

![](./media/image-20250709100329430.png)

| Ultrasone Sensor | Keyestudio 8833 Board |
| :--------------: | :-------------------: |
|       Vcc        |           V           |
|       Trig       |          D12          |
|       Echo       |          D13          |
|       Gnd        |           G           |

Sluit de servo aan (D10)

![](./media/image-20250709100626238.png)

| Servo  | Keyestudio 8833 Board |
| :----: | :-------------------: |
| Bruin  |           G           |
|  Rood  |         V(5V)         |
| Oranje |          D10          |

<span style="color: rgb(255, 76, 65);">**Wij gebruiken een 18650 lithiumbatterij met een puntige positieve pool, waarbij het vermogen en de capaciteit niet vereist zijn.**</span>

![](./media/image-20250709100841625.png)