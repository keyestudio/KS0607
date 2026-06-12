### Proyecto 11: Tanque Seguidor de Ultrasonidos


#### **(1)Descripción:**

En la lección anterior, aprendimos sobre el auto inteligente seguidor de luz. En esta lección, podemos combinar los conocimientos para construir un auto seguidor de ultrasonidos. En el proyecto, usamos sensores ultrasónicos para detectar la distancia entre el auto y el obstáculo al frente, y luego controlamos la rotación de los dos motores en función de estos datos para controlar los movimientos del auto inteligente.

La lógica específica del auto inteligente seguidor de ultrasonidos se muestra en la siguiente tabla:

|                        Detección                        |              Configuración              |
| :-----------------------------------------------------: | :-------------------------------: |
| La distancia (cm) entre el auto y el obstáculo al frente | Ajustar el ángulo del servo a 90° |
|                      **Condición**                      |           **Movimiento**            |
|               distancia≥20 y distancia≤50               |             Avanzar              |
|            10＜distancia＜20<br/>distancia＞50            |               Detener                |
|                       distancia≤10                       |              Retroceder              |

#### **(2)Diagrama de flujo:**

![](media/wps118.png)

#### **(3)Diagrama de conexión:**

![](media/c5c842ac7e834b9b24ab06b3ce3d02ac.png)

<span style="color: rgb(255, 76, 65);">Nota:</span> El cableado del sensor ultrasónico, el servo y el motor es el mismo que en el experimento del proyecto anterior. El GND, VCC, SDA y SCL del panel LED 8x16 están conectados respectivamente a G (GND), V (VCC), A4 y A5 en la placa de expansión.

#### **(4)Código de prueba:**

También puedes arrastrar bloques para editar tu código, como se muestra a continuación.

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/f6fb93211f786d023eb77eb210eae454.png)

（3）![](media/5c5994681a5e494ba5ae4ce3c2d1ddac.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

(7) ![](media/4b40151c7482ff9371570978b8ef9c77.png)

(8) ![](media/ac663c190f6b0fe5e9861b29b94765b5.png)

(9) ![](media/72f725bac7ba927b55e3a9eea3b1a660.png)

(10) ![](media/fcad8e3c5bf2690dfc7ed07200f72401.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, ya que la carga del código también utiliza comunicación serie, y puede haber conflictos con la comunicación serie Bluetooth, lo que puede causar que la carga falle.)

![](media/b895ca60e3249e09d4c15c356c60099a.png)


#### **(5)Resultado de la prueba:**

Carga el código, enciende el dispositivo y mueve el interruptor DIP a ON. El servo rotará 90°, el panel LED 8X16 mostrará ![](media/fdd4ae50b3372cc9c4ef27f6bddda387.png), y el auto seguirá al obstáculo en movimiento.

![](./media/img-20240117093900.png)