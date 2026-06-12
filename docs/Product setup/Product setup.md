# 2. Instalación del Producto

<span style="color: rgb(255, 76, 65);">**Precaución**</span>: Establezca el ángulo inicial del servo y retire las películas delgadas de las placas antes de instalar este robot.

![](./media/image-20250709092645945.png)

 **Paso 1**

![KS0607_18](./media/KS0607_18.png)

![KS0607_19](./media/KS0607_19.png)

![KS0607_20](./media/KS0607_20.png)

Por favor, realice el cableado primero.

![](./media/image-20250709093344681.png)

![KS0607-099](./media/KS0607-099.jpg)

![KS0607_21](./media/KS0607_21.png)

![KS0607_22](./media/KS0607_22.png)

![KS0607_23](./media/KS0607_23.png)

**Paso 2**

![KS0607_24](./media/KS0607_24.png)

![KS0607_25](./media/KS0607_25.png)

![KS0607_26](./media/KS0607_26.png)

**Paso 3**

![KS0607_28](media\KS0607_28.png)

![KS0607_29](./media/KS0607_29-177909268352217.png)

![KS0607_30](./media/KS0607_30-177909269696918.png)

 **Paso 4**

![KS0607_31](./media/KS0607_31-17790915380363.png)

![KS0607_32](./media/KS0607_32-17790915471644.png)

![KS0607_33](./media/KS0607_33-17790915540415.png)

![KS0607_34](./media/KS0607_34-17790915654246.png)

![KS0607_35](./media/KS0607_35-17790915710247.png)



**Paso 5**

![KS0607_36](./media/KS0607_36-17790915806918.png)

<span style="color: rgb(255, 76, 65);">Observe la dirección de los puentes (jumper caps).</span>

![KS0607_37](./media/KS0607_37-17790915896649.png)

![KS0607_38](./media/KS0607_38-177909159600610.png)

 **Paso 6**

![KS0607_39](./media/KS0607_39.png)

![KS0607_40](./media/KS0607_40.png)

![KS0607_41](./media/KS0607_41.png)

**Paso 7**

![KS0607_42](./media/KS0607_42.png)

![KS0607_43](./media/KS0607_43.png)

![KS0607_44](./media/KS0607_44.png)

**Paso 8**

（Es necesario ajustar el ángulo del servo）

![KS0607-098](./media/KS0607-098.jpg)

![KS0607-097](./media/KS0607-097.jpg)

**Establezca el ángulo del servo en 90°**

Para ajustar el código del servo, selecciónelo según el curso.

1.**Arduino:** Descargue el archivo de código: [Arduino](./Arduino.7z)

![](./media/image-20250710110650230.png)

2.**Kidsblock:** Descargue el archivo de código: [Kidsblock](./Kidsblock.7z)

![](./media/image-20250710110906515.png)

**Después de inicializar el ángulo del servo, instale el módulo Bluetooth.**

Mantenga el sensor ultrasónico paralelo a la placa.

![KS0607-096](./media/KS0607-096.jpg)

![](./media/image-20250709095307371.png)

 **Paso 9**

![KS0607_48](./media/KS0607_48-177909161769011.png)

![KS0607_49](./media/KS0607_49-177909162425112.png)

![KS0607_50](./media/KS0607_50-177909163131113.png)

**Paso 10**

![KS0607_51](./media/KS0607_51-177909163803814.png)

![KS0607_52](./media/KS0607_52-177909164311315.png)

![KS0607_53](./media/KS0607_53-177909164907716.png)

**Cableado**

Para el panel LED 8\*16, conecte los cables a A4 y A5.

![](./media/image-20250709095552072.png)

![](./media/image-20250709095606248.png)

![](./media/image-20250709095643567.png)

Conecte el motor A al puerto A y el motor B al puerto B.

![](./media/image-20250709095728739.png)

![](./media/image-20250709095740866.png)

Conecte el cable de alimentación.

![](./media/image-20250709095759390.png)

![](./media/image-20250709095811580.png)

Sensor de seguimiento de línea (ver la imagen)

![](./media/image-20250709095830428.png)

![](./media/image-20250709095848550.png)

![](./media/image-20250709095901776.png)

![](./media/image-20250709095911639.png)

Cablee las fotorresistencias

![](./media/image-20250709095929779.png)

![](./media/image-20250709095939414.png)

| Fotorresistencia | Keyestudio 8833 Board |
| :--------------: | :-------------------: |
|        G         |           G           |
|        V         |           V           |
|        s         |          A1           |

![](./media/image-20250709100043670.png)

| Fotorresistencia | Keyestudio 8833 Board |
| :--------------: | :--------------------: |
|        G         |           G            |
|        V         |           V            |
|        S         |           V2           |

Cablee el sensor ultrasónico.

![](./media/image-20250709100317508.png)

![](./media/image-20250709100329430.png)

| Sensor Ultrasónico | Keyestudio 8833 Board |
| :----------------: | :-------------------: |
|        Vcc         |           V           |
|        Trig        |          D12          |
|        Echo        |          D13          |
|        Gnd         |           G           |

Cablee el servo (D10)

![](./media/image-20250709100626238.png)

| Servo   | Keyestudio 8833 Board |
| :-----: | :-------------------: |
| Marrón  |           G           |
|  Rojo   |         V(5V)         |
| Naranja |          D10          |

<span style="color: rgb(255, 76, 65);">**Utilizamos una batería de litio modelo 18650 con polo positivo en punta, cuya potencia y capacidad no son requisitos estrictos.**</span>

![](./media/image-20250709100841625.png)