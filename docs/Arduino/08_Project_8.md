### Proyecto 8: Control de Motor y Velocidad

#### **(1)Descripción:**

Existen muchas formas de controlar motores. Nuestro carro inteligente utiliza la solución más común llamada L298P. El L298P, fabricado por STMicroelectronics, es un excelente chip de control especialmente diseñado para manejar motores de alta potencia.

Puede controlar directamente motores de corriente continua, motores de dos fases y cuatro fases con una corriente de control de hasta 2A. Y el terminal de salida del motor adopta 8 diodos Schottky de alta velocidad como protección.

Hemos diseñado una placa de expansión basada en el circuito L298P cuyo diseño apilable puede conectarse directamente a la placa UNO R3, reduciendo las dificultades técnicas para los usuarios al usar y controlar el motor.

Apile la placa de expansión sobre la placa, alimente la BAT, gire el interruptor DIP al extremo ON y alimente la placa de expansión y la placa UNO R3 al mismo tiempo mediante una fuente de alimentación externa.

Para facilitar el cableado, la placa de expansión está equipada con interfaz anti-inversión (PH2.0 -2P -3P -4P -5P) y por lo tanto puede conectarse directamente con motores, fuente de alimentación y sensores/módulos.

La interfaz Bluetooth de la placa de expansión de control es totalmente compatible con el módulo Bluetooth Keyestudio HM-10. Por lo tanto, solo necesitamos insertar el módulo Bluetooth HM-10 en la interfaz correspondiente al conectarlo.

Al mismo tiempo, la placa de extensión de control también usa conectores de pines 2.54 para extender algunos puertos digitales y analógicos disponibles, de modo que pueda continuar añadiendo otros sensores y realizar experimentos de expansión.

La placa de expansión puede conectarse a 4 motores de corriente continua. En el modo de conexión predeterminado con jumper, los motores de las interfaces A y A1, B y B1 están conectados en paralelo y su patrón de movimiento es el mismo. Se pueden usar 8 jumpers para controlar la dirección de rotación de las 4 interfaces de motor.

Por ejemplo, cuando los dos jumpers frente a la interfaz del motor A cambian de una conexión horizontal a una conexión vertical, la dirección de rotación del motor A ahora es opuesta a la dirección original.

![](media/image-20230427081635216.png)

![](media/5381c98d3be6da099ce43e841b8f736b.png)

#### **(2)Parámetros：**

- Voltaje de entrada de la parte lógica: DC 5V

- Voltaje de entrada de la parte de control: DC 7-12V

- Corriente de trabajo de la parte lógica: ≤36mA

- Corriente de trabajo de la parte de control: ≤ 2A

- Potencia máxima de disipación: 25W (T=75℃)

- Nivel de entrada de señal de control:
  
  ​	Nivel alto: 2.3V ≤ Vin ≤ 5V
  
  ​	Nivel bajo: 0V ≤ Vin ≤ 1.5V

- Temperatura de trabajo: -25℃～＋130℃

#### **(3)Control del movimiento del robot**

El pin de dirección del motor A es D2, el pin de control de velocidad es D5; el pin de dirección del motor B es D4 y el pin de control de velocidad es D6.

De acuerdo con la tabla a continuación, podemos saber cómo controlar el movimiento del robot controlando la rotación de dos motores a través de los puertos digitales y puertos PWM. Entre ellos, el rango del valor PWM es 0-255. Cuanto mayor sea el valor, más rápido girará el motor.

|     Función      |  D4  | D6（PWM） | Motor（izquierdo）B |  D2  | D5（PWM） | Motor（derecho）A |
| :--------------: | :--: | :-------: | :-----------------: | :--: | :-------: | :---------------: |
| Avanzar          | HIGH |  255-200  |    Girar izquierda  | HIGH |  255-200  |   Girar izquierda |
| Retroceder       | LOW  |    200    |    Girar derecha    | LOW  |    200    |   Girar derecha   |
| Girar izquierda  | LOW  |    200    |    Girar derecha    | HIGH |  255-200  |   Girar izquierda |
| Girar derecha    | HIGH |  255-200  |    Girar izquierda  | LOW  |    200    |   Girar derecha   |
| Detener          | LOW  |     0     |       Detener       | LOW  |     0     |      Detener      |




#### **(4)Diagrama de Conexión:**

![](media/3e53cf19ea5f85a931b955453b86304b.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

El conector de 4 pines está marcado con A, A1, B1 y B. El motor trasero derecho está conectado a B de la placa 8833 y el delantero izquierdo está conectado al puerto A.

#### **(5)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.1
motor driver
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Definir el pin de control de dirección del motor izquierdo
#define ML_PWM 6 // Definir el pin de control PWM del motor izquierdo
#define MR_Ctrl 2 // Definir el pin de control de dirección del motor derecho
#define MR_PWM 5 // Definir el pin de control PWM del motor derecho

void setup()
{
    pinMode(ML_Ctrl, OUTPUT);// Definir el pin de control de dirección del motor izquierdo como OUTPUT
    pinMode(ML_PWM, OUTPUT);// Definir el pin de control PWM del motor izquierdo como OUTPUT
    pinMode(MR_Ctrl, OUTPUT);// Definir el pin de control de dirección del motor derecho como OUTPUT
    pinMode(MR_PWM, OUTPUT);// Definir el pin de control PWM del motor derecho como OUTPUT
}

void loop()
{
    // adelante
    digitalWrite(ML_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor izquierdo en HIGH
    analogWrite(ML_PWM, 55); // La velocidad de control PWM del motor izquierdo es 55
    digitalWrite(MR_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor derecho en HIGH
    analogWrite(MR_PWM, 55); // La velocidad de control PWM del motor derecho es 55
    delay(2000);// retardo de 2s

    // atrás
    digitalWrite(ML_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor izquierdo en LOW
    analogWrite(ML_PWM, 200); // La velocidad de control PWM del motor izquierdo es 200
    digitalWrite(MR_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor derecho en LOW
    analogWrite(MR_PWM, 200); // La velocidad de control PWM del motor derecho es 200
    delay(2000);// retardo de 2s

    // girar izquierda
    digitalWrite(ML_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor izquierdo en LOW
    analogWrite(ML_PWM, 200); // La velocidad de control PWM del motor izquierdo es 200
    digitalWrite(MR_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor derecho en HIGH
    analogWrite(MR_PWM, 55); // La velocidad de control PWM del motor derecho es 55
    delay(2000);// retardo de 2s

    // girar derecha
    digitalWrite(ML_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor izquierdo en HIGH
    analogWrite(ML_PWM, 55); // La velocidad de control PWM del motor izquierdo es 55
    digitalWrite(MR_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor derecho en LOW
    analogWrite(MR_PWM, 200); // La velocidad de control PWM del motor derecho es 200
    delay(2000);// retardo de 2s

    // detener
    digitalWrite(ML_Ctrl, LOW);
    analogWrite(ML_PWM, 0); // La velocidad de control PWM del motor izquierdo es 0
    digitalWrite(MR_Ctrl, LOW);
    analogWrite(MR_PWM, 0); // La velocidad de control PWM del motor derecho es 0
    delay(2000);// retardo de 2s
}
```

#### **(6)Resultados de la Prueba:**

Después de cablear según el diagrama, cargar el código de prueba y encenderlo.

![](./media/img-20240117082646.png)

el carro inteligente avanza durante 2s, retrocede durante 2s, gira a la izquierda durante 2s, gira a la derecha durante 2s y se detiene durante 2s, repitiendo esta secuencia.

#### **(7)Explicación del Código:**

**digitalWrite(ML_Ctrl,LOW);**

El cambio entre niveles alto y bajo puede hacer que los motores giren en sentido horario o antihorario. Los pines digitales generales pueden usarse para controlar estos movimientos.

**analogWrite(ML_PWM,200);**

El ajuste de velocidad del motor se realiza mediante PWM, y el pin que controla la velocidad del motor debe ser el pin PWM de Arduino.

#### **(8)Proyecto de Expansión:**

Ajustamos la velocidad de los motores controlando PWM y el cableado permanece igual.

**Código de Prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 8.2
motor driver pwm
http://www.keyestudio.com
*/

#define ML_Ctrl 4 // Definir el pin de control de dirección del motor izquierdo
#define ML_PWM 6 // Definir el pin de control PWM del motor izquierdo
#define MR_Ctrl 2 // Definir el pin de control de dirección del motor derecho
#define MR_PWM 5 // Definir el pin de control PWM del motor derecho

void setup() 
{
    pinMode(ML_Ctrl, OUTPUT);// Definir el pin de control de dirección del motor izquierdo como OUTPUT
    pinMode(ML_PWM, OUTPUT);// Definir el pin de control PWM del motor izquierdo como OUTPUT
    pinMode(MR_Ctrl, OUTPUT);// Definir el pin de control de dirección del motor derecho como OUTPUT
    pinMode(MR_PWM, OUTPUT);// Definir el pin de control PWM del motor derecho como OUTPUT
}

void loop() 
{
    // adelante
    digitalWrite(ML_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor izquierdo en HIGH
    analogWrite(ML_PWM, 155); // La velocidad de control PWM del motor izquierdo es 155
    digitalWrite(MR_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor derecho en HIGH
    analogWrite(MR_PWM, 155); // La velocidad de control PWM del motor derecho es 155
    delay(2000);// retardo de 2s

    // atrás
    digitalWrite(ML_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor izquierdo en LOW
    analogWrite(ML_PWM, 100); // La velocidad de control PWM del motor izquierdo es 100
    digitalWrite(MR_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor derecho en LOW
    analogWrite(MR_PWM, 100); // La velocidad de control PWM del motor derecho es 100
    delay(2000);// retardo de 2s

    // izquierda
    digitalWrite(ML_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor izquierdo en LOW
    analogWrite(ML_PWM, 100); // La velocidad de control PWM del motor izquierdo es 100
    digitalWrite(MR_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor derecho en HIGH
    analogWrite(MR_PWM, 155); // La velocidad de control PWM del motor derecho es 155
    delay(2000);// retardo de 2s

    // derecha
    digitalWrite(ML_Ctrl, HIGH); // Establecer la velocidad de control de dirección del motor izquierdo en HIGH
    analogWrite(ML_PWM, 155); // La velocidad de control PWM del motor izquierdo es 155
    digitalWrite(MR_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor derecho en LOW
    analogWrite(MR_PWM, 100); // La velocidad de control PWM del motor derecho es 100
    delay(2000);// retardo de 2s

    // detener
    digitalWrite(ML_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor izquierdo en LOW
    analogWrite(ML_PWM, 0); // La velocidad de control PWM del motor izquierdo es 0
    digitalWrite(MR_Ctrl, LOW); // Establecer la velocidad de control de dirección del motor derecho en LOW
    analogWrite(MR_PWM, 0); // La velocidad de control PWM del motor derecho es 0
    delay(2000);// retardo de 2s
}
```

Cargue el código, la velocidad del motor es más lenta.

Una corriente baja hará que el motor gire lentamente.