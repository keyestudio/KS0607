### Proyecto 20: Ventilador

#### **(1)Descripción：**

![](media/4afc1c9720d36beba8adfac0ee22ff10.png)

Este módulo de ventilador utiliza un chip de control de motor HR1124S, un chip controlador H-bridge de un solo canal que contiene transistores de potencia PMOS y NMOS de baja resistencia de conducción. La baja resistencia de conducción puede reducir el consumo de energía, contribuyendo al funcionamiento seguro del chip por más tiempo.

Además, su bajo consumo en espera y bajo consumo en estado estático lo hacen aplicable a juguetes. Podemos controlar la dirección de rotación y la velocidad del ventilador enviando señales IN+ e IN- y señales PWM.

#### **(2)Parámetros:**

- Voltaje de funcionamiento: 5V

- Corriente: 200mA

- Potencia máxima: 2W

- Temperatura de trabajo: -10 °C a +50 grados Celsius

- Tamaño: 47.6mm \* 23.8mm

#### **(3)Diagrama de conexión:**

El módulo de ventilador necesita ser impulsado por una corriente elevada; por lo tanto, instalamos un portapilas.

![](media/2bd9aa5cc21e274458328958561f1915.png)

Los pines GND, VCC, IN+ e IN- del módulo de ventilador se conectan a los pines G, V, 12 y 13 del shield.

#### **(4)Código de prueba:**

También puedes arrastrar bloques para editar tu código, como se muestra a continuación

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/1360090880c1cd9b20671c17604f4108.png)

![](media/4e9354e674060efe6cf540a3e1b87813.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de subir el código, porque la subida del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la subida falle.)

![](media/cbb8f153dd0d114bdd350577af7a1f02.png)

#### **(5)Resultados de la prueba:**

Sube el código, conecta los componentes, enciende el dispositivo y gira el interruptor DIP a ON. El pequeño ventilador girará en sentido horario durante 2s, se detendrá durante 2s y girará en sentido antihorario durante 2s.

![](./media/img-20240117100504.png)

#### **(6)Práctica de extensión:**

Hemos comprendido el principio de funcionamiento del sensor de llama. A continuación, conecta un sensor de llama en el circuito, como se muestra a continuación. Luego controla el ventilador para apagar el fuego con el sensor de llama.

![](media/67463007499fe6b3f077b4bfbdce6cad.png)


Puedes arrastrar bloques para editar tu código, como se muestra a continuación

![](media/4e9d7f8f92495db5208c718292da3e15.png)

![](media/337311907ec5e21f151b20c0e49e9ba9.png)

![](media/5b5e78e7acccddd6b278c52cf5d9a6bb.png)

![](media/cc09f61b782a662eaee267f8dbd8968d.png)

**Código de prueba completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de subir el código, porque la subida del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la subida falle.)

![](media/74ddb07daf4063f0640c31f4243a0864.png)


Después de subir el código, enciende el interruptor de alimentación del shield del motor, puedes encender el ventilador cuando se detecte llama desde el sensor de llama izquierdo del robot.

![](./media/img-20240117102303.png)