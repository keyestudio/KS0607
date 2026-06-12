### Proyecto 5: Control de Servo

#### **(1)Descripción:**

Un servomotor es un actuador rotativo de control de posición. Consiste principalmente en una carcasa, una placa de circuito, un motor sin núcleo, un engranaje y un sensor de posición. Su principio de funcionamiento es que el servo recibe la señal enviada por el MCU o receptor y produce una señal de referencia con un período de 20ms y un ancho de 1.5ms. Luego compara el voltaje de polarización de CC adquirido con el voltaje del potenciómetro y obtiene la salida de diferencia de voltaje.

Cuando la velocidad del motor es constante, el potenciómetro es accionado para girar a través del engranaje de reducción en cascada, lo que lleva a que la diferencia de voltaje sea 0 y el motor deje de girar. Generalmente, el rango de ángulo de rotación del servo es de 0° a 180°.

El ángulo de rotación del servomotor se controla regulando el ciclo de trabajo de la señal PWM (Modulación por Ancho de Pulso). El ciclo estándar de la señal PWM es de 20ms (50Hz). Teóricamente, el ancho se distribuye entre 1ms-2ms, pero en la práctica está entre 0.5ms-2.5ms. El ancho corresponde al ángulo de rotación de 0° a 180°. Tenga en cuenta que para diferentes marcas de motores, la misma señal puede resultar en diferentes ángulos de rotación.

![](media/69be958142b773acdae33eeef12afed7.png)

En general, el servo tiene tres cables: marrón, rojo y naranja. El cable marrón es la tierra, el rojo es el polo positivo y el naranja es la línea de señal.

![](media/49467dfa70799401a5a5acc691014aee.png)

El ángulo del servo:

![](media/ddc74f62dc936c925d28d70a1a9c2214.png)

#### **(2)Parámetros:**

- Voltaje de trabajo: DC 4.8V \~ 6V

- Rango de ángulo de operación: aproximadamente 180° (a 500 → 2500 μsec)

- Rango de ancho de pulso: 500 → 2500 μsec

- Velocidad sin carga: 0.12 ± 0.01 seg / 60 (DC 4.8V) 0.1 ± 0.01 seg / 60 (DC 6V)

- Corriente sin carga: 200 ± 20mA (DC 4.8V) 220 ± 20mA (DC 6V)

- Torque de parada: 1.3 ± 0.01kg · cm (DC 4.8V) 1.5 ± 0.1kg · cm (DC 6V)

- Corriente de parada: ≦ 850mA (DC 4.8V) ≦ 1000mA (DC 6V)

- Corriente en espera: 3 ± 1mA (DC 4.8V) 4 ± 1mA (DC 6V)

#### **(3)Diagrama de Conexión:**

![](media/5120d0b422a1d0b1f1ba075aa5911c25.png)

<span style="color: rgb(255, 76, 65);">Nota:</span> Los cables marrón, rojo y naranja del servo se conectan respectivamente a Gnd(G), 5v(V) y 10 del shield. Recuerde conectar una fuente de alimentación externa debido a la alta corriente del servo. De lo contrario, la placa de desarrollo se quemará.

#### **(4)Código de Prueba 1:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.1
Servo
http://www.keyestudio.com
*/

#define servoPin 10 //El pin del servo

int pos; //La variable del ángulo del servo
int pulsewidth; //La variable del ancho de pulso del servo

void setup() 
{
    pinMode(servoPin, OUTPUT); //Establecer el pin del servo como salida
    procedure(0); //Establecer el ángulo del servo en 0°
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  // De 1° a 180°
    {
    	// en pasos de 1 grado	
        procedure(pos); // Rotar al ángulo de 'pos'
        delay(15); //Controlar la velocidad de rotación
    }
    for (pos = 180; pos >= 0; pos -= 1) // De 180° a 1°
    { 
        procedure(pos); // Rotar al ángulo de 'pos'
        delay(15);
    }
}
//La función controla el servo
void procedure(int myangle) 
{
    pulsewidth = myangle * 11 + 500; //Calcular el valor del ancho de pulso
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth); //El tiempo en nivel alto representa el ancho de pulso
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000)); //Como el ciclo es 20ms, el tiempo restante está en nivel bajo
}
```

Al cargar el código, veremos que el servo se mueve de 0° a 180°. En los capítulos siguientes, introduciremos cómo controlar un servo. Además, podemos controlar un servo con una librería de servo de Arduino.

<span style="color: rgb(255, 76, 65);">Nota:</span> Este archivo de librería de servo utiliza el temporizador 1, y la salida PWM de los puertos IO 9 y 10 también utiliza el temporizador 1, por lo que no podemos usar esta librería de servo cuando usemos la salida PWM de D9 y D10 más adelante.

#### **(5)Código de Prueba 2:**

(<span style="color: rgb(255, 76, 65);">Nota: </span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial del Bluetooth, lo que puede causar que la carga del código falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 5.2
Servo
<http://www.keyestudio.com>
*/

#include <Servo.h>

Servo myservo; // crear servos
int pos = 0; // Guardar las variables del ángulo

void setup() 
{
	myservo.attach(10); //Conectar el servo con el puerto digital 10
}

void loop() 
{
    for (pos = 0; pos <= 180; pos += 1)  //De 0° a 180°
    {
    	//la longitud de paso es 1
        myservo.write(pos); // Rotar al ángulo de 'pos'
        delay(15); // Esperar 15ms para controlar la velocidad
    }

    for (pos = 180; pos >= 0; pos -= 1)  //De 180° a 0°
    {
        myservo.write(pos); // Rotar al ángulo de 'pos'
        delay(15); // Esperar 15ms para controlar la velocidad
    }
}
```

#### **(6)Resultados de la Prueba:**

Cargue el código, conecte la alimentación y el servo se moverá en el rango de 0° a 180°.

![](./media/img-20240117090810.png)

#### **(7)Explicación del Código:**

Arduino viene con **\#include \<Servo.h\>** (función y declaraciones del servo)

A continuación se presentan algunas declaraciones comunes de la función servo:

1\. **attach（interfaz）**——Establecer la interfaz del servo, los puertos 9 y 10 están disponibles

2\. **write（ángulo）**——La declaración para establecer el ángulo de rotación del servo, el rango de ángulo es de 0° a 180°

3\. **read（）**——La declaración para leer el ángulo del servo, lee el valor del comando de "write()"

4\. **attached（）**——Verificar si el parámetro del servo ha sido enviado a su interfaz

Nota: El formato de escritura anterior es "nombre de variable del servo, declaración específica（）", por ejemplo: myservo.attach(10)