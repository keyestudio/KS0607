### Proyecto 12: Tanque de Evasión de Obstáculos Ultrasónico

#### **(1)Descripción:**

En el proyecto anterior, hicimos un auto inteligente seguidor de sonido ultrasónico. De hecho, usando los mismos componentes y el mismo método de cableado, solo necesitamos cambiar el código de prueba para convertirlo en un auto inteligente de evasión de obstáculos ultrasónico. Este auto inteligente puede moverse con el movimiento de las manos humanas.

Usamos sensores ultrasónicos para detectar la distancia entre el auto inteligente y el obstáculo al frente, y luego controlamos la rotación de los dos motores basándonos en estos datos para controlar los movimientos del auto inteligente.

|                          Detección                           |         |
| :----------------------------------------------------------: | :-----: |
| Distancia medida por el sensor ultrasónico entre el auto y el obstáculo al frente <br />（establecer el ángulo del servo a 90°） | a (cm)  |
| Distancia medida por el sensor ultrasónico entre el auto y el obstáculo a la derecha <br />（establecer el ángulo del servo a 0°） | a2 (cm) |
| Distancia medida por el sensor ultrasónico entre el auto y el obstáculo a la izquierda <br />（establecer el ángulo del servo a 180°） | a1 (cm) |

**Configuración: establecer el ángulo inicial del servo a 90°**

| Condición 1 |        Condición 2         |      Condición 3       | Movimiento                                                     |
| :---------: | :------------------------: | :--------------------: | :----------------------------------------------------------- |
|    a＜20    |                            |                        | Detener 500ms；establecer el ángulo del servo a 180°，leer a1，retardo de 100ms；establecer el ángulo del servo a 0°，leer a2，retardo de 0.1s. |
|             | a1＜50<br />o<br />a2＜50 | **Comparar a1 con a2** |                                                              |
|             |                            |         a1＞a2         | Establecer el ángulo del servo a 90°，girar a la izquierda durante 700ms（establecer PWM a 255），y avanzar（establecer PWM a 200）. |
|             |                            |         a1＜a2         | Establecer el ángulo del servo a 90°，girar a la derecha durante 700ms（establecer PWM a 255），y avanzar（establecer PWM a 200）. |
|             | a1≥50<br />y<br />a2≥50  |         Aleatorio         | Establecer el ángulo del servo a 90°，girar a la izquierda durante 500ms（establecer PWM a 255），y avanzar（establecer PWM a 200）.<br /><br />Establecer el ángulo del servo a 90°，girar a la derecha durante 500ms（establecer PWM a 255），y avanzar（establecer PWM a 200）. |
|    a≥20     |                            |                        | Avanzar（establecer PWM a 100）                               |

#### **(2)Diagrama de flujo:**

![](media/wps119.png)

#### **(3)Diagrama de conexión:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

(<span style="color: rgb(255, 76, 65);">Nota:</span> los cables marrón, rojo y naranja del servo están conectados respectivamente a G (GND), V（5V）y D10 de la placa de expansión；y para el sensor ultrasónico, el pin VCC está conectado a 5v (V), el pin Trig al digital 12 (S), el pin Echo al digital 13 (S), y el pin Gnd a Gnd (G); igual que en el proyecto anterior.）

#### **(4)Código de prueba:**


También puedes arrastrar bloques para editar tu código, como se muestra a continuación.![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/5dcbd405806b8e341505d7316246dbdd.png)

（3）![](media/996c8d4e5dd9620757dfb097329e7d5d.png)

（4）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

（10）![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

（11）![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de subir el código, porque la subida del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la subida falle.)

![](media/4360f9642a8c6b2488767c079d481482.png)

#### **(5)Resultados de la prueba:**

Después de subir el código de prueba exitosamente, realiza el cableado, gira el interruptor DIP al extremo ON y enciende el dispositivo. El auto inteligente avanzará y evitará obstáculos automáticamente.

![](./media/img-20240117093950.png)