### Proyecto 16: Control Remoto por Bluetooth

![](./media/img-20240111140012.png)

#### **(1)Descripción:**

En las últimas décadas, Bluetooth se ha convertido en el módulo de comunicación inalámbrica más popular porque es fácil de usar y ha encontrado amplias aplicaciones en la mayoría de los dispositivos alimentados por baterías.

Con el fin de adaptarse a los tiempos, la realidad y las necesidades de los clientes, Bluetooth ha sido actualizado varias veces. En los últimos años, ha experimentado muchas transformaciones en términos de velocidad de transferencia de datos, consumo de energía en dispositivos portátiles y dispositivos IoT, sistemas de seguridad, entre otros. Aquí, planeamos aprender sobre el DX-BT24 con la placa Arduino.

#### **(2)Parámetros:**

- Protocolo Bluetooth: Bluetooth Specification V5.1 BLE

- Envío y recepción por puerto serie sin límite de bytes

- Distancia de comunicación: 40m (entorno abierto)

- Frecuencia de operación: banda ISM 2.4GHz

- Método de modulación: GFSK (Gaussian Frequency Shift Keying)

- Características de seguridad: Autenticación y Cifrado

- Servicios compatibles: UUIDs Central y Periférico FFE0, FFE1, FFE2

- Consumo de energía: modo de suspensión automática, corriente en espera 400uA\~800uA, 8.5mA durante la transmisión.
  
- Alimentación: 5V

- Temperatura de operación: –10 a +65 grados Celsius

#### **(3)Diagrama de Conexión:**

1.STATE es el pin de prueba de estado conectado al diodo emisor de luz interno y generalmente permanece sin conectar.

2.RXD es la interfaz del puerto serie para el terminal receptor.

3.TXD es la interfaz del puerto serie para el terminal de envío.

4.GND es para tierra.

5.VCC es el polo positivo.

6.EN/BRK: la desconexión de este representa la desconexión del Bluetooth y generalmente permanece sin conectar.

(Nota: aquí el Bluetooth está conectado directamente al shield V2 y **por favor preste atención a la dirección**)

![](media/63b96e5b26ee18337fb6e0dced5bbbe3.png)


#### **(4)Descargar e instalar la APP:**

##### **Para sistema IOS**

1\. Abra App Store.

2\. Busque <span style="color: rgb(61, 167, 66);">KeyesRobot</span> en la Apple Store y haga clic en descargar.

![](./media/img-20240111141301.png)

3\. Después de instalar la aplicación, verá el siguiente ícono en el escritorio de su teléfono.

![](./media/img-20240111141412.png)

**Cómo conectar el teléfono iOS al módulo Bluetooth:**

1\. Active el Bluetooth y los servicios de ubicación en el teléfono a través de la configuración.

![](./media/img-20240111141943.png)

2\. Permita que la APP KeyesRobot acceda al Bluetooth a través de la configuración.

![](./media/img-20240111142052.png)

3\. Haga clic para abrir la App KeyesRobot.

![](./media/img-20240111142140.png)

4\. KeyesRobot App es una APP universal, que se aplica a múltiples robots keyestudio. Si la interfaz no muestra "TANK ROBOT", puede hacer clic en los botones izquierdo y derecho para encontrar "TANK ROBOT".

5\. Haga clic en el botón <span style="color: rgb(61, 167, 66);">Bluetooth</span> ![](./media/img-20240111142336.png) en la esquina superior derecha para escanear el bluetooth

![](./media/img-20240111142415.png)

6\. Verá un Bluetooth llamado <span style="color: rgb(0, 209, 0);">**BT24**</span>, haga clic en el botón <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111142536.png)

7\. Si el LED integrado en el módulo Bluetooth deja de parpadear y permanece encendido, significa que su teléfono se ha conectado exitosamente al módulo Bluetooth.

![](./media/img-20240111142702.png)


##### **Para Sistema Android**

1\. Busque <span style="color: rgb(61, 167, 66);">**KeyesRobot**</span> en Google Play, o abra el siguiente enlace para descargar e instalar la aplicación.

[https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio](https://play.google.com/store/apps/details?id=com.keyestudio.keyestudio)

![](./media/img-20240111143312.png)

2\. Active el Bluetooth y los servicios de ubicación del teléfono móvil

![](./media/img-20240111143354.png)

3\. Encuentre la aplicación Bluetooth KeyesRobot en la configuración, haga clic en las opciones de permisos de la aplicación y
habilite los permisos de Ubicación y dispositivos cercanos.(<span style="color: rgb(255, 76, 65);">Nota:</span> Algunos teléfonos móviles no tienen la función de permisos de dispositivos cercanos.)

![](./media/img-20240111143451.png)

4\. Haga clic para abrir la App KeyesRobot.

![](./media/img-20240111143529.png)

5\. KeyesRobot App es una APP universal, que se aplica a múltiples robots keyestudio. Si la interfaz no muestra "TANK ROBOT", puede hacer clic en los botones izquierdo y derecho para encontrar "TANK ROBOT".

6\. Haga clic en el botón <span style="color: rgb(61, 167, 66);">Bluetooth</span> ![](./media/img-20240111142336.png) en la esquina superior derecha para escanear el bluetooth

![](./media/img-20240111142415.png)

7\. Verá un Bluetooth llamado <span style="color: rgb(0, 209, 0);">**BT24**</span>, haga clic en el botón <span style="color: rgb(255, 169, 0);">Connect</span>.

![](./media/img-20240111143910.png)

8\. Cuando su teléfono se haya conectado exitosamente al módulo Bluetooth, el LED integrado en el módulo Bluetooth dejará de parpadear y permanecerá encendido.

![](./media/img-20240111144004.png)

![](./media/img-20240111142702.png)


#### **(5)Probar la APP Bluetooth:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.1
Bluetooth
http://www.keyestudio.com
*/

char ble_val; // Variable de tipo caracter (usada para almacenar el valor recibido por Bluetooth)

void setup() 
{
	Serial.begin(9600);
}

void loop() 
{
    if (Serial.available() > 0) // Determinar si hay datos en el buffer del puerto serie
    {
        ble_val = Serial.read(); // Leer los datos en el buffer del puerto serie
        Serial.println(ble_val); // Imprimir
    }
}
```

Cargue el código en la placa de desarrollo, luego conecte el módulo Bluetooth, y después conecte el teléfono móvil al módulo Bluetooth.

Después de que el teléfono móvil se haya conectado exitosamente al módulo Bluetooth, haga clic para abrir la APP Bluetooth y haga clic en el botón <span style="color: rgb(0, 252, 255);">Select</span> en la <span style="color: rgb(0, 252, 255);">página principal</span>.

![](./media/img-20240111144744.png)

La interfaz principal de la aplicación Bluetooth se muestra en la figura a continuación.

![](./media/img-20240111144859.png)

Después de que el código anterior se haya cargado exitosamente, abra el monitor serial del arduino IDE y configure la velocidad de baudios a 9600. Haga clic en el ícono de la interfaz de la APP y el monitor serial mostrará el comando enviado por el botón.

![](media/805f8ee5c8998a5d6cb8bcef9da09186.png)

<br>
<br>
<span style="color: rgb(255, 76, 65);">**Nota: El método de conexión de la APP es el mismo que se describe a continuación.**</span>
<br>
<b>

#### **(6)Explicación del Código:**

**Serial.available()** representa el número de caracteres que quedan actualmente en el buffer del puerto serie.

Esta función generalmente se usa para determinar si hay datos en esta área. Cuando Serial.available()\>0, significa que el puerto serie ha recibido datos y puede ser leído.

**Serial.read()** se refiere a extraer y leer un Byte de datos del buffer del puerto serie. Por ejemplo, si un dispositivo envía datos al Arduino a través del puerto serie, podemos usar Serial.read() para leer los datos enviados.

#### **(7)Proyecto de Expansión:**

Aquí usamos el comando enviado por el teléfono móvil para encender o apagar una luz LED. Mirando el diagrama de cableado, un LED está conectado al pin D9.

![](media/549c10efcf47f29f8f6355d8cd0497cc.png)

**Código de Prueba**

(<span style="color: rgb(255, 76, 65);">Nota: </span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial del Bluetooth, lo que puede causar que la carga del código falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 16.2
Bluetooth
http://www.keyestudio.com
*/

int LED = 9;
char ble_val; // Variable entera usada para almacenar el valor recibido por Bluetooth

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT);
}

void loop() 
{

    if (Serial.available() > 0) // Determinar si hay datos en el buffer del puerto serie
    {
        ble_val = Serial.read(); // Leer datos del buffer del puerto serie
        Serial.print("DATA RECEIVED:");
        Serial.println(ble_val);
        if (ble_val == 'a') 
        {
            digitalWrite(LED, HIGH);
            Serial.println("led on");
        }
        if (ble_val == 'b') 
        {
            digitalWrite(LED, LOW);
            Serial.println("led off");
        }
    }
}
```

![](media/3577f17c526b1dc55d4f587ef95f2d08.png)

Después de que el código anterior se haya cargado exitosamente, abra el monitor serial del arduino IDE y configure la velocidad de baudios a 9600. Haga clic en ![](media/3fd6c998c0f665fb607a5827794b9bfe.png) para controlar el LED. Al hacer clic en él, se enviará el caracter a, y el LED se encenderá. Si se presiona este botón nuevamente, el LED se apagará.

![](./media/img-20240117094533.png)

![](media/b45c3c46391467218fe07003dbb2f3e3.png)

Debe retirar el módulo BT si termina los proyectos.