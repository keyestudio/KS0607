### Proyecto 15: Tanque con Control Remoto por Infrarrojos

![](./media/image-20250709134800790.png)

#### **(1)Descripción:**

El control remoto por infrarrojos es una de las aplicaciones de control remoto más comunes que se encuentra en motores eléctricos, ventiladores eléctricos y muchos otros electrodomésticos. En este proyecto, utilizamos los conocimientos aprendidos anteriormente para construir un coche inteligente con control remoto por infrarrojos.

En la lección 9, probamos el valor de tecla correspondiente a cada botón del control remoto por infrarrojos. En este proyecto, podemos configurar el código (valor de tecla) para que el botón correspondiente controle los movimientos del coche inteligente y muestre los patrones de movimiento en la matriz de LED 8X16.

La lógica específica del coche inteligente se muestra en la tabla a continuación:

|                 Tecla ultrasónica                  | Valor de tecla | Instrucciones de las teclas                                       |
| :---------------------------------------------: | :-------: | ------------------------------------------------------------ |
| ![](media/b11dc5ffa6cccebc6088e5d557d76daf.png) |  FF629D   | Avanzar（establecer PWM en 200）<br />mostrar el patrón de avance |
| ![](media/ae8110034aacb083151cfd882ee599ba.png) |  FFA857   | Retroceder（establecer PWM en 200）<br />mostrar el patrón de retroceso |
| ![](media/bce9cba2c6d2465fbcce570ad4210eba.png) |  FF22DD   | Girar a la izquierda<br />mostrar el patrón"STOP"                     |
| ![](media/ad907a618af86f30d52986bbbd57ba76.png) |  FFC23D   | Girar a la derecha<br />mostrar el patrón de giro a la izquierda          |
| ![](media/9716a4ed61a4064d2f47a7b73eccaf87.png) |  FF02FD   | Detener<br />mostrar el patrón"STOP"                          |

**Configuración inicial: la matriz de LED 8X16 muestra el patrón"![](media/dc59c5fcb4fcf6af4d4a5ebb14b7a919.png)"**



#### **(2)Diagrama de flujo:**

![](media/wps121.png)

#### **(3)Diagrama de conexión:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA y SCL del panel LED 8x16 están conectados a G（GND), V（VCC). A4 y A5 de la placa de expansión.

Dado que la placa 8833 integra el receptor IR, no es necesario cablearlo. Los pines del receptor IR son G（GND), V（VCC) y D3.

#### **(4)Código de prueba:**

Puedes editar bloques para construir tu código

（1）![](media/949a82a4516f57a5e65fdbbd944dc860.png)

（2）![](media/1f98f44522f0d08b8d41a81109f91bee.png)

(3) ![](media/a9042e77ebe3009fbb7653bef3429b66.png)

（4）![](media/53c2dbc1af206a888f95f58b31000ab2.png)

（5）![](media/863962ed6e2fd7112e1b59265320c7f4.png)

（6）![](media/51e30aa2aca3a7da67ee4f0f81c7dad1.png)

（7）![](media/ce8358153ae79fb76937f3c22c935ae9.png)

（8）![](media/7ab62148fa2a23259b8039475978d8fc.png)

（9）![](media/3af2546fe93dc84ed3c3002543ae8069.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serie, y puede haber conflictos con la comunicación serie Bluetooth, lo que puede provocar que la carga falle.)

![](media/fae6c22640ced038daca9cb6721ab95e.png)

#### **(5)Resultados de la prueba:**

Después de cargar el código de prueba correctamente y encender el dispositivo, el coche inteligente puede controlarse para moverse mediante el control remoto IR y la pantalla 8\*16 muestra los patrones correspondientes a sus movimientos.

![](./media/img-20240117094223.png)