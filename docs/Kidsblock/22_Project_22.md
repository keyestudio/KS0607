### Proyecto 22: Múltiples Funciones del Robot Extintor de Incendios

#### **(1)Descripción:**

El coche inteligente ha realizado una sola función en cada proyecto anterior.

¿Puede mostrar múltiples funciones a la vez? Sí, puede.

En este último proyecto grande, pretendemos usar un código completo para controlar el coche inteligente y demostrar todas las funciones mencionadas en los proyectos anteriores. Usamos las teclas de la APP de Bluetooth para cambiar automáticamente entre varias funciones, lo cual es bastante simple y conveniente.

#### **(2)Diagrama de Flujo:**

<span style="color: rgb(255, 76, 65);">**Por favor, consulte el Proyecto 16 para instalar y configurar la APP de Bluetooth**</span>

![](media/wps122.png)

#### **(3)Diagrama de Conexión:**

![](media/e7ac834ba04aa2e8862995d2d33ce935.png)

1\. GND, VCC, SDA y SCL de la placa 8x16 están conectados a G (GND), + (VCC), A4 y A5 de la placa de expansión.

2\. VCC, IN+, IN- y Gnd del módulo de ventilador están conectados a 5V (V), 12 (S), 13 (S) y Gnd (G).

3\. El cable marrón, el cable rojo y el cable naranja del servo están conectados a Gnd (G), 5v (V) y D10.

4\. RXD, TXD, GND y VCC del módulo BT están conectados a TX, RX, G (GND) y 5V (VCC). STATE y BRK no necesitan ser conectados.

5\. Los pines "G", "V" y A del sensor de llama izquierdo están conectados a G (GND), V (VCC) y A1, respectivamente; El sensor de llama derecho está conectado a G (GND), V (VCC) y A2, respectivamente.

6\. Los puertos distales del sensor de seguimiento de línea son 11, 7 y 8.

#### **(4)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)
<span style="color: rgb(255, 76, 65);">**Nota:**</span> No puede acelerar el coche mediante la App.

![](media/b1527b806741e28e8f2af5107db505fe.png)


#### **(5)Resultado de la Prueba:**

Antes de cargar el código del programa, el módulo Bluetooth debe ser retirado; de lo contrario, la carga del código fallará.

Después de cargar el código exitosamente, active los servicios de ubicación en su dispositivo y luego conecte el módulo Bluetooth.

Una vez que el módulo Bluetooth esté conectado y encendido, y la APP móvil esté conectada exitosamente al Bluetooth, podemos usar la APP móvil para controlar el robot tanque.

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)