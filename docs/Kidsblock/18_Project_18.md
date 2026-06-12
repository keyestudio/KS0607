### Proyecto 18: Múltiples Funciones del Robot Tanque Ultrasónico

#### **(1) Descripción:**

El carro inteligente ha realizado una función individual en cada proyecto anterior.

¿Puede mostrar múltiples funciones al mismo tiempo? Sí, puede.

En este último proyecto grande, tenemos la intención de usar un código completo para controlar el carro inteligente y demostrar todas las funciones mencionadas en los proyectos anteriores. Usamos las teclas de la APP Bluetooth para cambiar automáticamente entre varias funciones, lo cual es bastante simple y conveniente.

#### **(2) Diagrama de Flujo:**

![](media/wps122.png)

#### **(3) Diagrama de Conexión:**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA y SCL de la placa 8x16 están conectados a G (GND), + (VCC), A4 y A5 de la placa de expansión.

2\. VCC, Trig, Echo y Gnd del sensor ultrasónico están conectados a 5V (V), 12 (S), 13 (S) y Gnd (G).

3\. El cable marrón, el cable rojo y el cable naranja del servo están conectados a Gnd (G), 5v (V) y D10.

4\. RXD, TXD, GND y VCC del módulo BT están conectados a TX, RX, G (GND) y 5V (VCC). STATE y BRK no necesitan ser conectados.

5\. Los pines "G", "V" y S del módulo fotorresistor izquierdo están conectados a G (GND), V (VCC) y A1, respectivamente; El módulo fotorresistor derecho está conectado a G (GND), V (VCC) y A2, respectivamente.

6\. Los puertos distales del sensor de seguimiento de línea son 11, 7 y 8.

#### **(4) Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

<span style="color: rgb(255, 76, 65);">**Nota:**</span> No puede acelerar el carro a través de la App.

![](media/e3c4c6cf504b1b9ea6fbae63f5fd9077.png)

#### **(5) Resultado de la Prueba:**

Antes de cargar el código del programa, el módulo Bluetooth debe ser removido; de lo contrario, la carga del código fallará.

Después de cargar el código exitosamente, active los servicios de ubicación en su dispositivo y luego conecte el módulo Bluetooth.

Una vez que el módulo Bluetooth esté conectado y encendido, y la APP móvil esté conectada exitosamente al Bluetooth, podemos usar la APP móvil para controlar el robot tanque.