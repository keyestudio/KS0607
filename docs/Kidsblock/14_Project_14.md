### Proyecto 14: Tanque Seguidor de Línea


#### **(1)Descripción:**

El proyecto anterior introdujo cómo confinar el automóvil inteligente para que se mueva dentro de un cierto espacio. En este proyecto, utilizaremos los conocimientos aprendidos anteriormente para convertirlo en un automóvil inteligente seguidor de línea. En el experimento, usamos el sensor de seguimiento de línea para detectar si hay una línea negra alrededor del automóvil inteligente, y luego controlamos la rotación de los dos motores según los resultados de la detección, para que el automóvil inteligente se mueva a lo largo de la línea negra.

La lógica específica del automóvil inteligente se muestra en la siguiente tabla:

|               Sensor               |                          Detección                           |
| :--------------------------------: | :----------------------------------------------------------: |
| Sensor de seguimiento de línea en el centro | Línea negra detectada: en nivel alto<br />Línea blanca detectada: en nivel bajo |
|  Sensor de seguimiento de línea a la izquierda  | Línea negra detectada: en nivel alto<br />Línea blanca detectada: en nivel bajo |
| Sensor de seguimiento de línea a la derecha  | Línea negra detectada: en nivel alto<br />Línea blanca detectada: en nivel bajo |

|                         Condición 1                          |                         Condición 2                          |   Movimiento   |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------: |
| El sensor de seguimiento de línea <br />en el centro <br />detecta la línea negra | El sensor de seguimiento de línea a la izquierda detecta la línea negra<br />el de la derecha detecta líneas blancas | Girar a la izquierda  |
| El sensor de seguimiento de línea <br />en el centro <br />detecta la línea negra | El sensor de seguimiento de línea a la izquierda detecta líneas blancas<br />el de la derecha detecta la línea negra | Girar a la derecha |
| El sensor de seguimiento de línea <br />en el centro <br />detecta la línea negra | Ambos sensores izquierdo y derecho detectan líneas blancas<br />Ambos sensores izquierdo y derecho detectan la línea negra | Avanzar |
| El sensor de seguimiento de línea<br />en el centro <br />detecta líneas blancas | El sensor de seguimiento de línea a la izquierda detecta la línea negra<br />el de la derecha detecta líneas blancas | Girar a la izquierda  |
| El sensor de seguimiento de línea<br />en el centro <br />detecta líneas blancas | El sensor de seguimiento de línea a la izquierda detecta líneas blancas<br />el de la derecha detecta la línea negra | Girar a la derecha |
| El sensor de seguimiento de línea<br />en el centro <br />detecta líneas blancas | Ambos sensores izquierdo y derecho detectan líneas blancas<br />Ambos sensores izquierdo y derecho detectan la línea negra |     Detener     |

#### **(2)Diagrama de flujo:**

![](media/wps11.png)

#### **(3)Diagrama de conexión:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Código de prueba:**

También puedes arrastrar bloques para editar tu código, como se muestra a continuación

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（4）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（5）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（6）![](media/595ee7b491d37a90afe34cec1a429783.png)

（7）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（8）![](media/fec93c7b8b089de709fd50575931519c.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/294ae4c01072e34b58a334912c90083a.png)


#### **(5)Resultados de la prueba:**

Después de cargar el código de prueba exitosamente y encender el dispositivo, el automóvil inteligente se mueve a lo largo de la línea negra.

![](./media/img-20240117094129.png)