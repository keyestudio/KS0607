### Proyecto 3: Fotoresistencia

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Descripción:**

La resistencia fotosensible es una resistencia especial hecha de un material semiconductor como un sulfuro o selenio, y también se recubre con una resina a prueba de humedad con efecto fotoconductivo. La resistencia fotosensible es más sensible a la luz ambiental; con diferentes intensidades de iluminación, la resistencia de la fotoresistencia es diferente. Usamos la resistencia fotosensible para diseñar el módulo de resistencia fotosensible.

La señal del módulo se conecta al puerto analógico del microcontrolador. Cuando la intensidad de la luz es mayor, el voltaje del puerto analógico es mayor, es decir, el valor de simulación del microcontrolador también es grande; por el contrario, cuando la intensidad de la luz es menor, el voltaje del puerto analógico es menor, es decir, el valor de simulación del microcontrolador también es pequeño.

De esta manera, podemos leer el valor analógico correspondiente usando el módulo de resistencia fotosensible y la intensidad de la luz en el entorno inductivo.

![](./media/image-20250709122809574.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parámetros:**

- Valor de resistencia de la resistencia fotosensible: 5K Ω - 0.5M

- Tipo de interfaz: puerto de simulación A0, A1

- Voltaje de trabajo: 3.3V-5V

- Espaciado entre pines: 2.54mm

#### **(3)Diagrama de Conexión:**

Lo que vamos a probar a continuación es el módulo fotoresistor en el lado izquierdo del robot.

![](./media/img-20240117091730.png)

El fotoresistor izquierdo está conectado a A1/P3 del escudo de control del motor.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)


#### **(4)Código de Prueba:**

También puedes arrastrar bloques para editar tu código, como se muestra a continuación.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/844a4e322ac2a3609e89d7e412406616.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/d4da0bd0c55e3580fa95782d50f6e540.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede provocar que la carga falle.)

![](media/f29c7da2238bcc2bc70cb4b2c773b50d.png)

#### **(5)Resultados de la Prueba:**

Carga el código en la placa de desarrollo. Haz clic en ![](media/9011f20d83897d7a5936793c4ae142fc.png) para configurar la velocidad de baudios a 9600. Al cubrirlo con tu mano, el valor disminuye; si no lo cubres, el valor aumenta.

![](media/53e2fc37ee5bb2c6ec187c309c431c47.png)



#### **(6)Práctica de Extensión:**

El código anterior solo lee el valor del fotoresistor. Podemos combinar el fotosensible y el LED para cambiar el LED. ¿Qué tal controlar el brillo del LED con él?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

PWM puede cambiar el brillo de la luz, es decir, el LED debe estar conectado al PWM de la placa de desarrollo.

Conecta el LED a D9 y mantén los demás pines sin cambios, luego editamos el código.

También puedes arrastrar bloques para editar tu código, como se muestra a continuación.

![](media/f3bb36c8d40016865672399259c7945d.png)

![](media/0df2da585a311e7b3312111533cd96a8.png)

![](media/b94c3789429c5fed4fd38467cb9792dd.png)

![](media/9ecdfd77e2a69dea5a8df04e7d56a13a.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede provocar que la carga falle.)

![](media/b23bcae806e8e27382b162909d30f3c0.png)

Carga el código en la placa de desarrollo, presionamos el fotoresistor para ver si el brillo de la luz LED ha cambiado.

![](./media/img-20240117091759.png)