### Proyecto 6: Sensor Ultrasónico

#### **(1) Descripción:**

![](media/0180b169a1c3b228394b43df704fac32.png)

El sensor ultrasónico HC-SR04 utiliza sonar para determinar la distancia a un objeto, similar a lo que hacen los murciélagos. Ofrece una excelente detección de rango sin contacto con alta precisión y lecturas estables en un paquete fácil de usar. Viene completo con módulos transmisores y receptores ultrasónicos.

El HC-SR04 o sensor ultrasónico se utiliza en una amplia gama de proyectos electrónicos para crear aplicaciones de detección de obstáculos y medición de distancias, así como otras aplicaciones variadas. Aquí presentamos el método sencillo para medir la distancia con Arduino y el sensor ultrasónico, y cómo usar el sensor ultrasónico con Arduino.

![](./media/image-20250709105712919.png)

#### **(2) Parámetros:**

- Alimentación: +5V DC

- Corriente en reposo: \<2mA

- Corriente de trabajo: 15mA

- Ángulo efectivo: \<15°

- Distancia de medición: 2cm – 400 cm

- Resolución: 0.3 cm

- Ángulo de medición: 30 grados

- Ancho de pulso de entrada del disparador: 10uS


#### **(3) El principio del sensor ultrasónico:**

Como se muestra en la imagen anterior, es como dos ojos. Uno es el extremo transmisor y el otro es el extremo receptor.

El módulo ultrasónico emitirá ondas ultrasónicas después de recibir una señal de disparo. Cuando las ondas ultrasónicas encuentran el objeto y se reflejan de vuelta, el módulo genera una señal de eco, por lo que puede determinar la distancia del objeto a partir de la diferencia de tiempo entre la señal de disparo y la señal de eco.

El tiempo t es el tiempo que tarda la señal emitida en encontrar el obstáculo y regresar. La velocidad de propagación del sonido en el aire es de aproximadamente 343 m/s, y distancia = velocidad × tiempo. Sin embargo, la onda ultrasónica se emite y regresa, lo que equivale a 2 veces la distancia. Por lo tanto, se debe dividir entre 2; la distancia medida por **la onda ultrasónica = (velocidad × tiempo)/2**

1. Método de uso y diagrama de temporización del módulo ultrasónico:

2. Establecer el tiempo de retardo del pin Trig del SR04 a al menos 10μs, lo que puede dispararlo para detectar la distancia.

3. Tras el disparo, el módulo enviará automáticamente ocho pulsos ultrasónicos de 40KHz y detectará si hay una señal de retorno. Este paso lo completará automáticamente el módulo.

4. Si la señal regresa, el pin Echo generará un nivel alto, y la duración del nivel alto es el tiempo desde la transmisión de la onda ultrasónica hasta su retorno.

![](media/image-20230426172540424.png)

Diagrama de circuito del sensor ultrasónico:

![](media/a25028af84d6c7c94382c2a907101241.jpeg)

#### **(4) Diagrama de conexión:**

![](media/d8fad040d3ab5abe247d6a8d1e08a13d.png)

<span style="color: rgb(255, 76, 65);">Nota:</span> Los pines VCC, Trig, Echo y Gnd del sensor ultrasónico están conectados respectivamente a 5v(V), 12(S), 13(S) y Gnd(G) del shield.

#### **(5) Código de prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.1
Ultrasonic sensor
http://www.keyestudio.com
*/

int trigPin = 12; // El pin Trig se conecta al 12
int echoPin = 13; // El pin Echo se conecta al 13
long duration, cm, inches;

void setup() 
{
    // Inicio del puerto serial
    Serial.begin(9600);// Establece la velocidad en baudios a 9600
    // Definir entrada y salida
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
}

void loop() 
{
    // Se da un pulso bajo corto para asegurar un pulso alto limpio
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Al menos dar un disparo de nivel alto de 10us
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // El tiempo en nivel alto equivale al intervalo de tiempo entre la transmisión y el retorno del sonido ultrasónico
    duration = pulseIn(echoPin, HIGH);
    // Convertir a distancia
    cm = (duration / 2) / 29.1; // convertir a centímetros
    inches = (duration / 2) / 74; // Convertir a pulgadas
    // Imprimir por el puerto serial
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    delay(50);
}
```

#### **(6) Resultados de la prueba:**

Cargue el código de prueba en la placa de desarrollo, abra el monitor serial y configure la velocidad en baudios a 9600. La distancia detectada se mostrará en cm y pulgadas. Cuando obstaculice el sensor ultrasónico con su mano, el valor de distancia mostrado será menor.

![](media/2ff018e5d9d631a32fce99eb9b4778be.png)

#### **(7) Explicación del código:**

**int trigPin = 12;** este pin está definido para transmitir ondas ultrasónicas, generalmente como salida.

**int echoPin = 13;** este está definido como el pin de recepción, generalmente como entrada.

**cm = (duration/2) / 29.1; inches = (duration/2) / 74; por 0.0135**

Podemos calcular la distancia usando la siguiente fórmula:

distancia = (tiempo de viaje/2) x velocidad del sonido

La velocidad del sonido es: 343m/s = 0.0343 cm/uS = 1/29.1 cm/uS

O en pulgadas: 13503.9in/s = 0.0135in/uS = 1/74in/uS

Necesitamos dividir el tiempo de viaje entre 2 porque debemos tener en cuenta que la onda fue enviada, golpeó el objeto y luego regresó al sensor.

#### **(8) Práctica de extensión:**


Acabamos de medir la distancia mostrada por el sensor ultrasónico. ¿Qué tal si controlamos el LED con la distancia medida? Intentémoslo y conectemos un módulo de luz LED al pin D9.

![](media/291ac1db0f38418772d11bb1786b7314.png)

**Código de prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 6.2
Ultrasonic LED
http://www.keyestudio.com
*/

int trigPin = 12; // Trig está conectado al 12
int echoPin = 13; // Echo está conectado al 13
int LED = 9;
long duration, cm, inches;

void setup() 
{
    // iniciar puerto serial
    Serial.begin (9600);// establecer velocidad en baudios a 9600
    // definir entrada y salida
    pinMode(trigPin, OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LED, OUTPUT);
}

void loop() 
{
    // Se da un pulso bajo corto para asegurar un pulso alto limpio
    digitalWrite(trigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);// Dar al menos un disparo de nivel alto de 10us
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);
    // La duración del nivel alto es el tiempo desde el lanzamiento hasta el retorno de la onda ultrasónica
    duration = pulseIn(echoPin, HIGH);
    // convertir a distancia
    cm = (duration / 2) / 29.1; // convertir a centímetros
    inches = (duration / 2) / 74; // convertir a pulgadas
    // imprimir por el puerto serial
    Serial.print(inches);
    Serial.print("in, ");
    Serial.print(cm);
    Serial.print("cm");
    Serial.println();
    if (cm >= 2 && cm <= 10) 
    {
    	digitalWrite(LED, HIGH);// encender el LED
    } 
    else 
    {
    	digitalWrite(LED, LOW); // apagar el LED
    }
    delay(50);
}
```

Cargue el código de prueba en la placa de desarrollo y bloquee el sensor ultrasónico con la mano, luego verifique si el LED está encendido.

![](./media/img-20240117090734.png)