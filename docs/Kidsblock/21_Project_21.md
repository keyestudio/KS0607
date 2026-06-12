### Proyecto 21: Tanque Extintor de Incendios

#### **(1)Descripción:**

La función de seguimiento de línea del tanque inteligente se explicó en el proyecto anterior. En este proyecto utilizamos el sensor de llama para crear un robot extintor de incendios.

Cuando el carro encuentra llamas, el motor del ventilador girará para apagar el fuego. Por supuesto, primero necesitamos reemplazar el sensor ultrasónico y los dos fotorresistores con un módulo de ventilador y sensores de llama.

La lógica específica del carro inteligente se muestra en la tabla a continuación:

| Sensor de Llama Izquierdo | Sensor de Llama Derecho | Estado                                                        |
| :-----------------------: | :---------------------: | :------------------------------------------------------------ |
|           ≤700            |          ≤700           | El carro se detiene, el ventilador comienza a girar para apagar la llama |
|           ≥700            |          ≥700           | El carro se detiene, el ventilador comienza a girar para apagar la llama |
|           ≥700            |          ≥700           | El carro se detiene, el ventilador comienza a girar para apagar la llama |
|           ＞700           |          ＞700          | El ventilador se detiene, el carro se mueve                   |

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
1）Este experimento requiere el uso de una fuente de fuego. Por favor, manténgala alejada de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo la supervisión de un adulto. Si no puede confirmar que está en condiciones seguras, abandone el experimento.
2）El sensor de llama no es resistente al fuego, por favor no lo queme directamente con llama.
Podemos controlar un LED externo con el sensor de llama. El LED sigue conectado a D9. Cuando se detecta fuego, el LED se encenderá.


#### **(2)Diagrama de flujo:**

![](media/wps120.png)

#### **(3)Diagrama de Conexión:**

![](media/c02e461ac7bdbab7fd14a19c453e08e4.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA y SCL del panel LED 8x16 están conectados a G（GND), V（VCC), A4 y A5.

G, V y A de los dos sensores de llama están conectados a G（GND), V（VCC), A1 y A2 de la placa de expansión.

#### **(4)Código de Prueba:**


También puede arrastrar bloques para editar su código, como se muestra a continuación

（1）![](media/6eb13569aaa7bf560f62049df28b51db.png)

（2）![](media/2e41c11455f595e98bd2f0f27bf4a291.png)

（3）![](media/2e3d4904d9605dfecb5736b4bf235ab2.png)

（4） ![](media/5aa8407b0ed182b18f227c8e1ec9a0b4.png)

（5） ![](media/4b40151c7482ff9371570978b8ef9c77.png)

（6）![](media/c0365237fa7ec7de10e9fc465353fae1.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, ya que la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/c07c09e5533a37838722b8c2b513646d.png)

#### **(5)Resultados de la Prueba:**

Después de cargar el código de prueba exitosamente, encienda el dispositivo y gire el interruptor DIP al extremo ON. El carro inteligente apagará el fuego cuando detecte una llama.

![](media/2de5f1d832d40c0fc94274f1d87443c6.jpeg)

<span style="color: rgb(255, 76, 65);">**Nota:**</span>
Por favor, manténgalo alejado de materiales inflamables para prevenir incendios. Los niños deben experimentar bajo la supervisión de un adulto. Si no puede confirmar que está en condiciones seguras, abandone el experimento. El sensor de llama no es resistente al fuego, por favor no lo queme directamente con llama.