### Proyecto 16: Control Remoto por Bluetooth

![](./media/image-20250709134858245.png)

#### **(1)Descripción:**

En las últimas décadas, Bluetooth se ha convertido en el módulo de comunicación inalámbrica más popular, ya que es fácil de usar y ha encontrado amplias aplicaciones en la mayoría de los dispositivos alimentados por baterías.

Con el fin de adaptarse a los tiempos, la realidad y las necesidades de los clientes, Bluetooth ha sido actualizado varias veces. En los últimos años, ha experimentado muchas transformaciones en términos de velocidad de transferencia de datos, consumo de energía de dispositivos wearables y dispositivos IoT, sistemas de seguridad y otros aspectos. Aquí, planeamos aprender sobre el DX-BT24 con la placa Arduino.

#### **(2)Parámetros:**

- Protocolo Bluetooth: Bluetooth Specification V5.1 BLE
- Distancia de trabajo: En un entorno abierto, alcanza una distancia ultra larga de 40m
- Frecuencia de operación de comunicación: Banda ISM de 2.4GHz
- Interfaz de comunicación: UART
- Certificación Bluetooth: cumple con los estándares de certificación FCC CE ROHS REACH
- Parámetros del puerto serie: 9600, 8 bits de datos, 1 bit de parada, bit inválido, sin control de flujo
- Alimentación: 5V DC
- Temperatura de operación: –10 a +65 grados Celsius


#### **(3)Aplicación:**

El módulo DX-BT24 también admite el protocolo BT5.1 BLE, que puede conectarse directamente a dispositivos iOS con función Bluetooth BLE, y admite la ejecución residente de programas en segundo plano. Se utiliza principalmente en el campo de la transmisión inalámbrica de datos a corta distancia. Evita engorrosas conexiones de cables y puede reemplazar directamente los cables seriales. Áreas de aplicación exitosas de los módulos BT24:

※ Transmisión inalámbrica de datos Bluetooth;

※ Teléfonos móviles, equipos periféricos de computadora;

※ Equipos POS de mano;

※ Transmisión inalámbrica de datos de equipos médicos;

※ Control de hogar inteligente;

※ Impresora Bluetooth;

※ Juguetes de control remoto Bluetooth;

※ Bicicletas compartidas;

#### **(4)Descripción de pines:**

![](media/cd97cf79ff5cdd5bbd78f4cc960d38e5.png)

①STATE：pin de estado

②RX：pin de recepción

③TX：pin de envío

④GND：tierra

⑤VCC：pin de alimentación

⑥EN：pin de habilitación

Conectar Bluetooth a la placa de desarrollo

| Uno  | BT24 |
| :--: | :--: |
|  TX  |  RX  |
|  RX  |  TX  |
| VCC  |  5V  |
| GND  | GND  |

#### **(5)Diagrama de Conexión:**

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)

#### **(6)Descargar APP:**

##### **Para sistema iOS**

1\. Abrir App Store.

2\. Buscar <span style="color: rgb(61, 167, 66);">KeyesRobot</span> en la App Store de Apple y hacer clic en descargar.

![](./media/img-20240111141301.png)

3\. Una vez instalada la aplicación, verás el siguiente icono en el escritorio de tu teléfono.

![](./media/img-20240111141412.png)

**Cómo conectar el teléfono iOS al módulo Bluetooth:**

1\. Activar el Bluetooth y los servicios de ubicación en el teléfono a través de la configuración.

![](./media/img-20240111141943.png)

2\. Permitir que la APP KeyesRobot acceda al Bluetooth a través de la configuración.

![](./media/img-20240111142052.png)

3\. Hacer clic para abrir la App KeyesRobot.

![](./media/img-20240111142140.png)

4\. La App KeyesRobot es una APP universal que se aplica a múltiples robots de keyestudio. Si la interfaz no muestra "TANK ROBOT", puedes hacer clic en los botones izquierdo y derecho para encontrar "TANK ROBOT".

5\. Hacer clic en el <span style="color: rgb(61, 167, 66);">botón Bluetooth</span>![](./media/img-20240111142336.png) en la esquina superior derecha para escanear el bluetooth.

![](./media/img-20240111142415.png)

6\. Verás un Bluetooth llamado <span style="color: rgb(0, 209, 0);">**BT24**</span>, hacer clic en el botón <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111142536.png)

7\. Si el LED integrado en el módulo Bluetooth deja de parpadear y permanece encendido, significa que tu teléfono se ha conectado exitosamente al módulo Bluetooth.

![](./media/img-20240111142702.png)


##### **Para Sistema Android**

1\. Buscar <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> en Google Play, o abrir el siguiente enlace para descargar e instalar la aplicación.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Activar el Bluetooth y los servicios de ubicación del teléfono móvil.

![](./media/img-20240111143354.png)

3\. Buscar la aplicación Bluetooth KeyesRobot en la configuración, hacer clic en las opciones de permisos de la aplicación y habilitar los permisos de Ubicación y dispositivos cercanos. (<span style="color: rgb(255, 76, 65);">Nota:</span> Algunos teléfonos móviles no tienen la función de permisos de dispositivos cercanos.)

![](./media/img-20240111143451.png)

4\. Hacer clic para abrir la App KeyesRobot.

![](./media/img-20240111143529.png)

5\. La App KeyesRobot es una APP universal que se aplica a múltiples robots de keyestudio. Si la interfaz no muestra "TANK ROBOT", puedes hacer clic en los botones izquierdo y derecho para encontrar "TANK ROBOT".

6\. Hacer clic en el <span style="color: rgb(61, 167, 66);">botón Bluetooth</span>![](./media/img-20240111142336.png) en la esquina superior derecha para escanear el bluetooth.

![](./media/img-20240111142415.png)

7\. Verás un Bluetooth llamado <span style="color: rgb(0, 209, 0);">**BT24**</span>, hacer clic en el botón <span style="color: rgb(255, 169, 0);">Connect</span>.![](./media/img-20240111143910.png)

8\. Cuando tu teléfono se conecte exitosamente al módulo Bluetooth, el LED integrado en el módulo Bluetooth dejará de parpadear y permanecerá encendido.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(7)Código de Prueba BT:**

También puedes arrastrar bloques para editar tu código, como se muestra a continuación

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/19a90ffb7565966f7d40462abed876a7.png)

（5）![](media/c8228c5040a43ae322612b312c995ac3.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/4766ada3bf48bb35522f292d9352bb78.png)


Carga el código en la placa de desarrollo, luego conecta el módulo Bluetooth, y después conecta el teléfono móvil al módulo Bluetooth.

Después de que el teléfono móvil se conecte exitosamente al módulo Bluetooth, hacer clic para abrir la APP Bluetooth y hacer clic en el botón <span style="color: rgb(0, 252, 255);">Select</span> en la <span style="color: rgb(0, 252, 255);">página de inicio</span>.

![](./media/img-20240111144744.png)

La interfaz principal de la aplicación Bluetooth se muestra en la figura a continuación.

![](./media/img-20240111144859.png)

Hacer clic en ![Img](./media/img-20240111171312.png) y establecer la velocidad en baudios a 9600. Hacer clic en el icono en la interfaz de la APP y el monitor serial mostrará el comando enviado por el botón.

![](media/f5004f5334fb4885ac0096f99e4133f9.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Nota: El método de conexión de la APP es el mismo que se describe a continuación.**</span>
<br>
<br>


#### **(8)Práctica de Extensión:**

En el proyecto anterior, Bluetooth recibe la señal enviada por el teléfono móvil y la muestra en el puerto serie de la placa de desarrollo. Aquí usamos el comando enviado por el teléfono móvil para encender o apagar un LED. Observando el diagrama de cableado, un LED está conectado al pin D9.

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)


También puedes arrastrar bloques para editar tu código, como se muestra a continuación

（1）![](media/2a66a7e8b37c68ddc51cfdb3aff53ac2.png)

（2）![](media/96f38f571f4ecae87e8bd6175ac0ca2d.png)

（3）![](media/044ea8429f8bffd438d70f8a7976b663.png)

（4）![](media/aa78663af261ff1d9bc8ffa6ad7a65bc.png)

(5）![](media/c8228c5040a43ae322612b312c995ac3.png)

（6）![](media/4164bcf66d3d2415f43a0efcd1ce4243.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/91fd9d6f85e291fe90a63e5095ed7f44.png)

Después de que el código anterior se cargue exitosamente. Hacer clic en ![](media/d5e59839bafc63f8b35c78c60573d1fc.png) para controlar el LED.

![](./media/img-20240117094418.png)


Una vez que termines el proyecto BT, retíralo.