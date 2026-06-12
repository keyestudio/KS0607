### Proyecto 10: Tanque Seguidor de Luz


#### **(1)Descripción:**

En proyectos anteriores, presentamos detalladamente el uso de varios sensores, módulos y placas de expansión en el carro inteligente. Ahora pasemos a los proyectos del carro inteligente. Los carros inteligentes seguidores de luz, como su nombre lo indica, son carros inteligentes que pueden seguir la luz.

Podemos combinar el conocimiento de los proyectos de fotorresistor y accionamiento de motor para crear un carro inteligente buscador de luz. En el proyecto, usamos dos módulos fotorresistores para detectar la intensidad de luz en los lados izquierdo y derecho del carro inteligente, leemos los valores analógicos correspondientes y luego controlamos la rotación de los dos motores basándonos en estos dos datos para controlar así los movimientos del carro inteligente.

La lógica específica del carro inteligente seguidor de luz se muestra a continuación.

![image-20230525113331422](media/image-20230525113331422.png)

#### **(2)Diagrama de flujo:**

![](media/wps117.png)

#### **(3)Diagrama de conexión:**

![](media/d8132c5a3f88a1016d27e5fa9e5fda92.png)

<span style="color: rgb(255, 76, 65);">Nota: </span>Los pines "G", "V" y S del módulo fotorresistor izquierdo están conectados a G (GND), V (VCC) y A1 respectivamente;

Los pines "G", "V" y S del módulo fotorresistor derecho están conectados a G (GND), V (VCC) y A2 respectivamente.

El cable de 4 pines está marcado con A, A1, B1 y B. El motor trasero derecho está conectado al puerto B de la placa de expansión controladora de motor 8833 y el motor delantero izquierdo está conectado al puerto A de la placa de expansión controladora de motor 8833.

#### **(4)Código de prueba:**


También puedes arrastrar bloques para editar tu código, como se muestra a continuación.

（1）![](media/9352e6447f9648efddc7d5a748618332.png)

（2）![](media/1d99d71f5fe52dd2145cb11d75cabb21.png)

（3）![](media/5004e509325dffb32c05afe25abedfc9.png)

（4）![](media/6c6f0492f657c4c78a0497bb86519561.png)

（5）![](media/b8fc70fa8b3f335dcdf0c8ad9ed998c6.png)

（6）![](media/9eb0e93fbd43aa24f2ce656191f7cd79.png)

(7) ![](media/9f023e6f571e597e661a8d71a7f803cb.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">Nota:</span> El umbral 650 en el código puede ajustarse apropiadamente según la intensidad de luz específica.

No conectes el módulo Bluetooth antes de cargar el código, ya que la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial del Bluetooth, lo que puede provocar que la carga del código falle.)

![](media/6300174b85f63c05dbdcb3b77188f9dc.png)


#### **(5)Resultados de la prueba:**

Después de cargar el código de prueba con éxito, realiza el cableado, cambia el interruptor DIP al extremo ON y enciende el dispositivo; el carro inteligente sigue la luz para moverse.

![](./media/img-20240117093758.png)