### Proyecto 5: Control de Servo

#### **(1)Descripción:**

Un servomotor es un actuador rotativo de control de posición. Consiste principalmente en una carcasa, una placa de circuito, un motor sin núcleo, un engranaje y un sensor de posición. Su principio de funcionamiento es que el servo recibe la señal enviada por el MCU o receptor y produce una señal de referencia con un período de 20ms y un ancho de 1.5ms. Luego compara el voltaje de polarización de CC adquirido con el voltaje del potenciómetro y obtiene la salida de diferencia de voltaje.

Cuando la velocidad del motor es constante, el potenciómetro se acciona para girar a través del engranaje reductor en cascada, lo que hace que la diferencia de voltaje sea 0, y el motor deja de girar. En general, el rango de ángulo de rotación del servo es de 0° a 180°.

El ángulo de rotación del servomotor se controla regulando el ciclo de trabajo de la señal PWM (Modulación por Ancho de Pulso). El ciclo estándar de la señal PWM es de 20ms (50Hz). Teóricamente, el ancho se distribuye entre 1ms-2ms, pero en realidad está entre 0.5ms-2.5ms. El ancho corresponde al ángulo de rotación de 0° a 180°. Tenga en cuenta que para diferentes marcas de motores, la misma señal puede resultar en diferentes ángulos de rotación.

![](media/69be958142b773acdae33eeef12afed7.png)

En general, el servo tiene tres cables en marrón, rojo y naranja. El cable marrón es la conexión a tierra, el rojo es el cable de polo positivo y el naranja es el cable de señal.

![](media/49467dfa70799401a5a5acc691014aee.png)

El ángulo del servo:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parámetros:**

- Voltaje de funcionamiento: DC 4.8V \~ 6V

- Rango de ángulo de operación: aproximadamente 180 ° (a 500 → 2500 μsec)

- Rango de ancho de pulso: 500 → 2500 μsec

- Velocidad sin carga: 0.12 ± 0.01 seg / 60 (DC 4.8V) 0.1 ± 0.01 seg / 60 (DC 6V)

- Corriente sin carga: 200 ± 20mA (DC 4.8V) 220 ± 20mA (DC 6V)

- Par de detención: 1.3 ± 0.01kg · cm (DC 4.8V) 1.5 ± 0.1kg · cm (DC 6V)

- Corriente de detención: ≦ 850mA (DC 4.8V) ≦ 1000mA (DC 6V)

- Corriente en espera: 3 ± 1mA (DC 4.8V) 4 ± 1mA (DC 6V)

#### **(3)Diagrama de Conexión:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">**Nota:**</span> Los cables marrón, rojo y naranja del servo se conectan respectivamente a Gnd(G), 5v(V) y D10 del shield. Recuerde conectar una fuente de alimentación externa debido a la alta corriente del servo. De lo contrario, la placa de desarrollo se quemará.

#### **(4)Código de Prueba:**

También puede arrastrar bloques para editar su código, como se muestra a continuación

![](media/5b04350e0310955ee2ecd48338f556a3.png)

![](media/7dd97d17b785de17e6c9362fa32e2a74.png)

![](media/69724a2063fa25e0f142e1eb48efd40f.png)

![](media/e149b45054fe94196dea220b319cb0bf.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/26e37037daf84d69320b76dd13346cd1.png)

#### **(6)Resultados de la Prueba:**

Cargue el código, conecte la alimentación y el servo se mueve en el rango de 0° a 180°.

![](./media/img-20240117092225.png)