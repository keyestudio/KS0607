### Proyecto 8: Control de Motor y Velocidad

#### **(1)Descripción:**

Hay muchas formas de controlar motores. Nuestro carro inteligente utiliza la solución más común llamada L298P. L298P, producido por STMicroelectronics, es un excelente chip de control especialmente diseñado para manejar motores de alta potencia. Puede controlar directamente motores DC, motores de dos y cuatro fases con una corriente de control que alcanza los 2A. Además, el terminal de salida del motor adopta 8 diodos Schottky de alta velocidad como protección. Hemos diseñado una placa de expansión basada en el circuito L298P cuyo diseño apilado puede conectarse directamente a la placa UNO R3 para su uso, reduciendo las dificultades técnicas para los usuarios al utilizar y controlar el motor.

Apile la placa de expansión sobre la placa, alimente el BAT, gire el interruptor DIP al extremo ON, y alimente la placa de expansión y la placa UNO R3 al mismo tiempo mediante una fuente de alimentación externa. Para facilitar el cableado, la placa de expansión está equipada con interfaces anti-inversión (PH2.0 -2P -3P -4P -5P) y por lo tanto puede conectarse directamente con motores, fuente de alimentación y sensores/módulos. La interfaz Bluetooth de la placa de expansión de control es totalmente compatible con el módulo Bluetooth Keyestudio HM-10. Por lo tanto, solo necesitamos insertar el módulo Bluetooth HM-10 en la interfaz correspondiente al conectarlo. Al mismo tiempo, la placa de extensión de control también utiliza cabezales de pines 2.54 para extender algunos puertos digitales y analógicos disponibles, de modo que pueda continuar añadiendo otros sensores y llevar a cabo experimentos de expansión.

La placa de expansión puede conectarse a 4 motores DC. En el modo de conexión del capuchón de puente predeterminado, los motores de las interfaces A y A1, B y B1 están conectados en paralelo, y su patrón de movimiento es el mismo. Se pueden usar 8 capuchones de puente para controlar la dirección de rotación de las 4 interfaces de motor. Por ejemplo, cuando los dos capuchones de puente frente a la interfaz del motor A se cambian de una conexión horizontal a una conexión vertical, la dirección de rotación del motor A ahora es opuesta a la dirección de rotación original.

![](media/6c3731f639e113c8f32fe1829f239898.png)

![](media/62ee9578858ecc8e27b824af65fb22bb.png)

#### **(2)Parámetros:**

-   Voltaje de entrada de la parte lógica: DC 5V

-   Voltaje de entrada de la parte de control: DC 7-12V

-   Corriente de trabajo de la parte lógica: ≤36mA

-   Corriente de trabajo de la parte de control: ≤ 2A

-   Potencia máxima de disipación: 25W (T=75℃)

-   Nivel de entrada de señal de control:

    Nivel alto: 2.3V ≤ Vin ≤ 5V

    Nivel bajo: 0V ≤ Vin ≤ 1.5V

-   Temperatura de trabajo: -25℃～＋130℃

#### **(3)Control del movimiento del robot:**

El pin de dirección del motor A es D2, el pin de control de velocidad es D5; el pin de dirección del motor B es D4 y el pin de control de velocidad es D6.

Según la tabla a continuación, podemos saber cómo controlar el movimiento del robot controlando la rotación de dos motores a través de los puertos digitales y puertos PWM. Entre estos, el rango del valor PWM es 0-255. Cuanto mayor sea el valor, más rápido girará el motor.

|   Función    |  D4  | D6（PWM） | Motor（izquierdo）B |  D2  | D5（PWM） | Motor（derecho）A |
| :----------: | :--: | :-------: | :-----------------: | :--: | :-------: | :---------------: |
| Avanzar      | HIGH |     0     |   Gira a la izquierda   | HIGH |     0     |   Gira a la izquierda   |
| Retroceder   | LOW  |    255    |  Gira a la derecha  | LOW  |    255    |  Gira a la derecha  |
| Girar a la izquierda  | LOW  |    255    |  Gira a la derecha  | HIGH |    100    |   Gira a la izquierda   |
| Girar a la derecha | HIGH |    100    |   Gira a la izquierda   | LOW  |    255    |  Gira a la derecha  |
|   Detener    | LOW  |     0     |      Se detiene     | LOW  |     0     |      Se detiene     |

#### **(4)Diagrama de Conexión:**

![](./media/image-20250709134029403.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

El conector de 4 pines está marcado con A, A1, B1 y B. El motor trasero derecho está conectado a B de la placa 8833 y el frontal izquierdo está conectado al puerto A.

#### **(5)Código de Prueba:**

También puede arrastrar bloques para editar su código, como se muestra a continuación.

（1）![](media/7cbc4d14c2e2dac956f2e9f145f01f31.png)

（2）![](media/0067d367772d4e3005bfc097ba3b59b0.png)

（3）![](media/f0c505e8268454c7996b755f97c6322b.png)

（4）![](media/b7215c8a4997a188947e80fdee1a8cd9.png)

**Código de Prueba Completo**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

![](media/332229f3dc01a38de898367f52531b28.png)


#### **(6)Resultados de la Prueba:**

Después de cablear según el diagrama, cargar el código de prueba y encenderlo.

![](./media/img-20240117092625.png)

el carro inteligente avanza durante 2s, retrocede durante 2s, gira a la izquierda durante 2s, gira a la derecha durante 2s y se detiene durante 2s.