### Proyecto 3: Fotorresistor

![](media/36e7e08764ed3c61a1c22f86be8c23d9.jpeg)

#### **(1)Descripción:**

La resistencia fotosensible es una resistencia especial fabricada con un material semiconductor como un sulfuro o selenio, y también está recubierta con una resina a prueba de humedad con efecto fotoconductivo. La resistencia fotosensible es más sensible a la luz ambiental, con diferentes intensidades de iluminación, y la resistencia de la resistencia fotosensible es diferente. Utilizamos la resistencia fotosensible para diseñar el módulo de resistencia fotosensible.

La señal del módulo está conectada al puerto analógico del microcontrolador. Cuando la intensidad de la luz es mayor, mayor es el voltaje del puerto analógico, es decir, el valor de simulación del microcontrolador también es mayor; por el contrario, cuando la intensidad de la luz es menor, menor es el voltaje del puerto analógico, es decir, el valor de simulación del microcontrolador también es menor.

De esta manera, podemos leer el valor analógico correspondiente usando el módulo de resistencia fotosensible, y la intensidad de la luz en el entorno inductivo.

![](media/7784e14e15402644cdbe674d500327c4.png)

![](media/0d9daba6454ef099fe1ceb0e6cb56ec4.png)

#### **(2)Parámetros:**

Valor de resistencia de la resistencia fotosensible: 5K Ou-0.5m

Tipo de interfaz: puerto de simulación A0, A1

Voltaje de trabajo: 3.3V-5V

Espaciado entre pines: 2.54mm


#### **(3)Diagrama de Conexión:**

Lo que vamos a probar a continuación es el módulo fotorresistor en el lado izquierdo del robot.

![](./media/img-20240117091559.png)

El fotorresistor izquierdo está conectado a A1/P3 del escudo del motor.

![](media/484852a36f52bdbe44bec1b9a8941e44.png)

#### **(4)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.1

photocell

http://www.keyestudio.com

*/

int sensorPin = A1; // A1 es el pin de entrada del fotorresistor

int sensorValue = 0; // guarda el valor del fotorresistor

void setup() 
{
	Serial.begin(9600); // Abre el monitor del puerto serial y establece la velocidad en baudios a 9600
}

void loop() 
{
	sensorValue = analogRead(sensorPin); // Lee el valor analógico del sensor fotorresistor
	Serial.println(sensorValue); // El puerto serial imprime el valor del fotorresistor
	delay(500); // Retardo de 500ms
}
```

#### **(5)Resultados de la Prueba:**

![](media/54b92578e3210999e23f5fb8138f0fa0.png)

Al cubrirlo, el valor disminuye; si no, el valor aumenta.

#### **(6)Explicación del Código:**

**analogRead(sensorPin)**: lee el valor analógico del fotorresistor

**Serial.begin(9600)**: inicializa el puerto serial y establece la velocidad en baudios a 9600

**Serial.println**: imprime por serial

#### **(7)Práctica de Extensión:**

El código anterior solo lee el valor del fotorresistor. Podemos hacer que el fotosensible y el LED se combinen para cambiar el LED. ¿Qué tal controlar el brillo del LED con él?

![](media/88a89f7996fb7f7d037315e57e8bcd33.png)

El brillo del LED está controlado por PWM. Por lo tanto, conectamos el LED al pin PWM (pin 9) del escudo.

**Código de Prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```c
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 3.2

photocell-analog output

http://www.keyestudio.com

*/

int analogInPin = A1; // A1 es el pin de entrada del fotorresistor

int analogOutPin = 9; // El puerto digital 9 es la salida del PWM

int sensorValue = 0; // guarda la variable del valor de resistencia del fotorresistor

int outputValue = 0; // Valor de salida al PWM

void setup() 
{
	Serial.begin(9600); // Abre el monitor del puerto serial y establece la velocidad en baudios a 9600
}

void loop() 
{
    sensorValue = analogRead(analogInPin); // Lee el valor analógico del sensor fotorresistor
    // Mapea los valores analógicos 0\~1023 a los valores de salida PWM 255\~0
    outputValue = map(sensorValue, 0, 1023, 255, 0);
    // Cambia la salida analógica
    analogWrite(analogOutPin, outputValue);
    Serial.println(sensorValue); // El puerto serial imprime el valor del fotorresistor
    delay(2);
}
```

Carga el código en la placa de desarrollo, luego cubre el fotorresistor y observa el brillo del LED.

![](./media/img-20240117091105.png)