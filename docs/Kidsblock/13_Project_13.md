### Proyecto 13: Tanque Moviéndose en un Espacio Confinado


#### **(1)Descripción:**

Las funciones de seguimiento ultrasónico y evasión de obstáculos del carro inteligente se han presentado en proyectos anteriores. Aquí, tenemos la intención de combinar el conocimiento de los cursos anteriores para confinar el movimiento del carro inteligente dentro de un cierto espacio. En el experimento, usamos el sensor de seguimiento de línea para detectar si hay una línea negra alrededor del carro inteligente, y luego controlamos la rotación de los dos motores según los resultados de la detección, de modo que el carro inteligente quede bloqueado dentro de un círculo dibujado con una línea negra.

La lógica específica del carro inteligente se muestra en la tabla a continuación:

![](media/image-20230525114604923.png)

|                         Condición                         |                         Movimiento                          |
| :-------------------------------------------------------: | :-------------------------------------------------------: |
| Si uno de los tres sensores de seguimiento de línea detecta líneas negras | Retroceder（establecer PWM en 150）Luego girar a la izquierda（establecer PWM en 150） |
|             Ninguno de ellos detecta líneas negras              |               Avanzar（establecer PWM en 100）                |

#### **(2)Diagrama de flujo**

![](media/b3c30f92cb78d4c2a4a8bd746aef24e1.png)

#### **(3)Diagrama de Conexión:**

![](media/34c48ca77307761e5ce0b1a1fb202201.png)

#### **(4)Código de Prueba:**

También puedes arrastrar bloques para editar tu código, como se muestra a continuación

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/e48288f5b46e3e1c78489cb9d9b86333.png)

（3）![](media/801d176b32bc87904b8545ecf80874fc.png)

（4）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

（5）![](media/904732a3bfdb65a5ef0207d40b3abcc6.png)

（6）![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（7）![](media/595ee7b491d37a90afe34cec1a429783.png)

（8）![](media/4b40151c7482ff9371570978b8ef9c77.png)

（9）![](media/b919eb2b47ee87ae36e21099e754e8a1.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/e656126c11bb8ebe7b6b0df8f22e7a79.png)

#### **(5)Resultados de la Prueba:**

Después de cargar el código de prueba exitosamente y encender el dispositivo, el carro inteligente se mueve dentro de un círculo dibujado con una línea negra.

![](./media/img-20240117094034.png)