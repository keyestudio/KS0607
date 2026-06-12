### Proyecto 1: Parpadeo de LED

#### (1)Descripción：

![](./media/image-20250709122631704.png)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Para principiantes y entusiastas, el parpadeo de LED es un programa fundamental. LED, la abreviación de diodos emisores de luz, está compuesto por compuestos químicos de Ga, As, P, N, entre otros. El LED puede parpadear en diversos colores modificando el tiempo de retardo en el código de prueba. Al controlar, se alimenta GND y VCC. El LED se encenderá si el extremo S está en nivel alto; de lo contrario, se apagará.

#### **(2)Parámetros:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Interfaz de control: puerto digital
- Voltaje de trabajo: DC 3.3-5V
- Espaciado de pines: 2.54mm
- Color de visualización del LED: amarillo

#### (3)Componentes Requeridos:

![](./media/image-20250709122437613.png)

#### **(4)Placa de Expansión del Driver de Motor 8833:**

La placa de expansión del driver de motor Keyestudio 8833 es compatible con la placa de desarrollo Arduino UNO. Simplemente apílela sobre la placa de desarrollo al usarla.

![](media/d8696e83ade31f2b7c56cc5911eacbd7.GIF)

#### **(5)Diagrama de Conexión:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](./media/image-20250709122655936.png)

<span style="color: rgb(255, 76, 65);">**NOTA:**</span> El LED está conectado al puerto D9. Recuerde instalar los puentes en el shield.

#### **(6)Código de Prueba:**

También puede arrastrar bloques para editar su código, como se muestra a continuación.

![](media/cc43ba357acb68a4961adb7e5041b6fe.png)

![](media/26b69cd46ad24e1c900c4fb316430353.png)

![](media/21dc3c24da4271aa7ec2bfdac732eeb3.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de subir el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/ba4723bab640078eccbe1811da138bc3.png)

#### **(7)Resultados de la Prueba:**

Suba el programa; el LED parpadea con un intervalo de 1s.

#### **(8)Práctica de Extensión:**

Ya sabemos cómo controlar el LED, entonces cambiemos la frecuencia del LED.

Podemos cambiar la frecuencia del LED sin cambiar el pin del LED. Modifiquemos el código.

También puede arrastrar bloques para editar su código, como se muestra a continuación.

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de subir el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/58c76be4c719a885afb500e8f3b80b85.png)

El resultado de la prueba muestra que el LED parpadea más rápido. Por lo tanto, podemos concluir que los pines y el tiempo de retardo afectan la frecuencia de parpadeo.