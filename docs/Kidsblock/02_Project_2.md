### Proyecto 2: Ajustar el Brillo del LED

#### **(1)Descripción:**

En la lección anterior, controlamos el LED encendiéndolo y apagándolo para que parpadeara.

En este proyecto, controlaremos el brillo del LED a través de PWM simulando un efecto de respiración. De igual manera, puedes cambiar el tamaño del paso y el tiempo de retardo en el código para demostrar diferentes efectos de respiración.

PWM es un medio para controlar la salida analógica a través de medios digitales. El control digital se utiliza para generar ondas cuadradas con diferentes ciclos de trabajo (una señal que cambia constantemente entre niveles alto y bajo) para controlar la salida analógica.

En general, los voltajes de entrada de los puertos son 0V y 5V. ¿Qué pasa si se requieren 3V? ¿O un cambio entre 1V, 3V y 3.5V? No podemos estar cambiando resistencias constantemente. Por esta razón, recurrimos al PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Para las salidas de voltaje de los puertos digitales de Arduino, solo existen niveles BAJO y ALTO, que corresponden a las salidas de voltaje de 0V y 5V respectivamente. Puedes definir BAJO como "0" y ALTO como "1", y hacer que Arduino produzca quinientos "0" o "1" dentro de 1 segundo. Si produce quinientos "1", eso es 5V; si todos son "0", eso es 0V; si produce 250 patrones de 01, eso es 2.5V.

Este proceso puede compararse con ver una película. Las películas que vemos no son completamente continuas. En realidad, generan 25 imágenes por segundo, lo cual no puede ser percibido por los ojos humanos. Por lo tanto, lo percibimos como un proceso continuo. El PWM funciona de la misma manera. Para generar diferentes voltajes, necesitamos controlar la proporción de 0 y 1. Cuantos más "0" o "1" se produzcan por unidad de tiempo, más preciso será el control.

#### **(2)Parámetros:**

![](media/0ea85307e1317c25f2a8d92f25319aa8.png)

- Interfaz de control: Puerto digital 3

- Voltaje de trabajo: DC 3.3-5V

- Espaciado entre pines: 2.54mm

- Color de visualización del LED: amarillo

#### **(3)Diagrama de Conexión**

Los pines PWM de Arduino están conectados a 3, 5, 6, 9, 10 y 11. Mantén el pin9 sin cambios.

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4)Código de Prueba:**

También puedes arrastrar bloques para editar tu código, como se muestra a continuación

![](media/de8ccd3cb6621f0eb89a8514a9fd8452.png)

![](media/659b8a45b8e8d271226d9a25034aedfd.png)

![](media/3157917e305c01f1920cf4d06aff4ff9.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/aaab53a06684ab078936ee61f9abcbb3.png)


#### **(5)Resultados de la Prueba**

Una vez cargado el código de prueba exitosamente, el LED cambia gradualmente de brillante a oscuro, como la respiración humana, en lugar de encenderse y apagarse de inmediato.

#### **(6)Práctica de Extensión:**

Modifiquemos el valor del retardo y mantengamos el pin sin cambios, luego observemos cómo cambia el LED.

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/2ff0d71c2688d39695b760a1d0f76965.png)

Carga el código en la placa de desarrollo, el LED parpadea más lentamente.