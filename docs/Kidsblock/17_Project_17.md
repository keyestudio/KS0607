### Proyecto 17: Control de Tanque por Bluetooth

#### **(1)Descripción:**

Hemos aprendido los conocimientos básicos sobre Bluetooth en el proyecto anterior. En esta lección, usaremos Bluetooth para controlar el carro inteligente. Dado que involucra Bluetooth, se necesitan un extremo emisor y un extremo receptor. En el proyecto, usamos el teléfono móvil como emisor (maestro), y el carro inteligente conectado con el módulo Bluetooth HM-10 (esclavo) como receptor.

Aprendimos anteriormente que enviar un bit puede controlar LEDs. Y el principio de controlar este robot carro es el mismo.

Para controlar mejor el robot tanque inteligente, hemos creado especialmente una APP. En esta lección, leeremos todos los valores de las teclas en esta APP a través del código, y luego presentaremos la APP exclusiva de nuestro robot tanque.

#### **(2)Función de las Teclas en la APP:**

La siguiente tabla ilustra las funciones de las teclas correspondientes:

|                      Teclas                       |                                                |                          Funciones                           |
| :---------------------------------------------: | :--------------------------------------------: | :----------------------------------------------------------: |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) |                                                | Emparejar y conectar el módulo Bluetooth HM-10; hacer clic de nuevo para desconectar |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) |                                                |                 Seleccionar el robot a operar                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) |                                                |       Controlar los movimientos del robot mediante botones       |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) |                                                |      Controlar los movimientos del robot mediante joystick       |
| ![](media/3ab61154b4ae730a3757f40171846825.png) |                                                |       Controlar los movimientos del robot mediante gravedad       |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) |   Envía "F" al presionar y "S" al soltar    | El carro avanza cuando se presiona y se detiene cuando se suelta |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) |   Envía "L" al presionar y "S" al soltar    | El carro gira a la izquierda cuando se presiona y se detiene cuando se suelta |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) |   Envía "R" al presionar y "S" al soltar    | El carro gira a la derecha cuando se presiona y se detiene cuando se suelta |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) |   Envía "B" al presionar y "S" al soltar    | El carro retrocede cuando se presiona y se detiene cuando se suelta |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) |        Envía "u"+dígito+"\#" al arrastrar         |          Arrastrar para cambiar la velocidad del motor izquierdo          |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) |        Envía "v"+dígito+"\#" al arrastrar         |         Arrastrar para cambiar la velocidad del motor derecho          |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) |         Seleccionar para entrar a la página de Funciones          |                                                              |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Envía "G" al presionar y "S" al presionar de nuevo | Entra en modo de evitación de obstáculos al presionar y sale al presionar de nuevo |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Envía "h" al presionar y "S" al presionar de nuevo | Entra en modo de seguimiento al presionar y sale al presionar de nuevo |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Envía "e" al presionar y "S" al presionar de nuevo | Entra en modo de seguimiento de línea al presionar y sale al presionar de nuevo |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Envía "f" al presionar y "S" al presionar de nuevo | Entra en modo de movimiento en espacio confinado al presionar y sale al presionar de nuevo |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Envía "i" al presionar y "S" al presionar de nuevo | Entra en modo de seguimiento de luz al presionar y sale al presionar de nuevo |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Envía "j" al presionar y "S" al presionar de nuevo | Entra en modo de extinción de incendios al presionar y sale al presionar de nuevo |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Seleccionar para entrar al modo de visualización de expresiones faciales |                                                              |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Envía "k" al presionar y "z" al presionar de nuevo | Muestra patrón de sonrisa al hacer clic y borra la expresión al hacer clic de nuevo |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Envía "l" al presionar y "z" al presionar de nuevo | Muestra patrón de disgusto al hacer clic y borra la expresión al hacer clic de nuevo |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Envía "m" al presionar y "z" al presionar de nuevo | Muestra cara feliz al hacer clic y borra la expresión al hacer clic de nuevo |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Envía "n" al presionar y "z" al presionar de nuevo | Muestra patrón triste al hacer clic y borra la expresión al hacer clic de nuevo |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Envía "o" al presionar y "z" al presionar de nuevo | Muestra patrón despectivo al hacer clic y borra la expresión al hacer clic de nuevo |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Envía "p" al presionar y "z" al presionar de nuevo | Muestra patrón en forma de corazón al hacer clic y borra la expresión al hacer clic de nuevo |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) |                                                | Elegir para entrar a la interfaz de funciones personalizadas; hay seis teclas 1,2,3,4,5,6; con estas teclas, puedes ampliar algunas funciones por ti mismo |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) |               Hacer clic para enviar "w"                | Hacer clic para mostrar el valor analógico detectado por la fotorresistencia izquierda |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) |                Hacer clic para enviar "y"                | Hacer clic para mostrar el valor analógico detectado por la fotorresistencia derecha |
| ![](media/a76df707b84409e57a1167889c3510d9.png) |                Hacer clic para enviar "x"                | Hacer clic para mostrar la distancia detectada por el sensor ultrasónico (unidad: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Hacer clic para enviar "c" <br />Hacer clic de nuevo para enviar "d"  |   Presionar para encender el ventilador y presionar de nuevo para apagarlo    |

#### **(3)Diagrama de Flujo:**

![](./media/image-20250709135203165.png)

#### **(4)Diagrama de Conexión:**

![](media/930a8024364e07505e845624a94c27bd.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA y SCL del panel LED 8x16 están conectados a G（GND), V（5V), A4 y A5 de la placa de expansión. STATE y BRK no necesitan ser conectados. El módulo BT se inserta en la placa de expansión.

#### **(5)Código de Prueba:**

Puedes arrastrar bloques para editar tu código

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/3b4fb768cbf7e0b80fa55cb15aa932b7.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6) ![](media/8a13abc40d27d0470902e528b40170c3.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/341e0a01bd6a76edb53f9414ef641a75.png)

#### **(6)Resultado de la Prueba:**

Después de cargar el código, conecta el robot al módulo Bluetooth y empareja la APP Bluetooth. Enciende el interruptor de alimentación del escudo del motor. Coloca el robot en el suelo, puedes usar estos botones de la APP Bluetooth para controlar el robot.

![](media/352d5ec83c4246b980da10b5f99711c5.jpeg)

1. Las flechas hacia arriba, abajo, izquierda y derecha controlan el robot para moverse hacia adelante, hacia atrás, a la izquierda y a la derecha respectivamente.

![](./media/img-20240117095015.png)

2. Haz clic en el botón de joystick y arrastra la dirección del punto negro dentro del círculo blanco para controlar la dirección de movimiento del robot.

![](./media/img-20240117095052.png)

3. Haz clic en el botón de Gravedad e inclina el teléfono en las direcciones hacia adelante, hacia atrás, a la izquierda y a la derecha, y el robot se moverá en la dirección hacia la que se inclina el teléfono.

![](./media/img-20240117095131.png)