### Proyecto 4: Sensor de Seguimiento de Línea

#### **(1)Descripción:**

![](media/d37c24e508361ab86b019135ab6950a9.png)

El sensor de seguimiento es en realidad un sensor infrarrojo. El componente utilizado aquí es el tubo infrarrojo TCRT5000.

Su principio de funcionamiento es utilizar la diferente reflectividad de la luz infrarroja a los colores, luego convertir la intensidad de la señal reflejada en una señal de corriente.

Durante el proceso de detección, el negro está activo en nivel ALTO mientras que el blanco está activo en nivel BAJO. La altura de detección es de 0-3 cm.

El módulo de seguimiento de línea de 3 canales de Keyestudio ha integrado 3 conjuntos de tubos infrarrojos TCRT5000 en una sola placa, lo que resulta más conveniente para el cableado y el control.

Si el Sensor de Seguimiento de Línea no funciona como se esperaba, necesitará usar un destornillador para ajustar su potenciómetro y hacerlo más sensible. Cuando su dedo se acerca al sensor, el LED integrado en la placa se enciende, y cuando su dedo se aleja, el LED integrado se apaga. En este momento, su sensibilidad es relativamente buena.

![](./media/img-20240117090858.png)

#### **(2)Parámetros:**

- Voltaje de operación: 3.3-5V (DC)

- Interfaz: 5PIN

- Señal de salida: Señal digital

- Altura de detección: 0-3 cm


Nota especial: antes de realizar las pruebas, gire el potenciómetro del sensor para ajustar la sensibilidad de detección. Cuando el LED se ajuste en el umbral entre ENCENDIDO y APAGADO, la sensibilidad es la mejor.

<span style="color: rgb(255, 76, 65);">Nota:</span> el sensor de seguimiento de línea está instalado en la parte inferior del robot.

#### **(3)Diagrama de Conexión:**

![](media/6426516400b21d7fbe1d9a1a58a1808b.png)

#### **(4)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.1

Line Track sensor

http://www.keyestudio.com

*/

// Cableado de los sensores de seguimiento de línea

#define L_pin 11 // izquierdo
#define M_pin 7 // central
#define R_pin 8 // derecho

void setup()
{
    Serial.begin(9600); // Establecer la tasa de baudios a 9600
    pinMode(L_pin, INPUT); // Establecer todos los pines de los sensores de seguimiento de línea en modo entrada
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Leer el valor del sensor izquierdo
    int M_val = digitalRead(M_pin); // Leer el valor del sensor central
    int R_val = digitalRead(R_pin); // Leer el valor del sensor derecho

    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // retardo de 100ms
}
```

#### **(5)Resultados de la Prueba:**

Cargue el código en la placa de desarrollo, abra el monitor serial para verificar los sensores de seguimiento de línea. El valor mostrado es 1 (nivel alto) cuando no se reciben señales. El valor cambia a 0 cuando el sensor está cubierto con papel.

![](./media/img-20240117090920.png)


![](media/b9319753c148f66aabc9bf648ed93da1.png)

#### **(6)Explicación del Código:**

**Serial.begin(9600)**- Inicializar el puerto serial, establecer la tasa de baudios a 9600

**pinMode-** Definir el pin como modo de entrada o salida

**digitalRead-** Leer el estado del pin, que generalmente son nivel ALTO y BAJO

#### **(7)Práctica de Extensión:**

Después de conocer su principio de funcionamiento, puede conectar un LED a D9, para controlar el LED mediante el sensor de seguimiento de línea.

![](media/1dd733ed6248d09e9b4d218e41559294.png)

**Código de Prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 4.2

Line Track sensor

http://www.keyestudio.com

*/

// Pin del LED
#define LED 9
// Cableado de los sensores de seguimiento de línea
#define L_pin 11 // izquierdo
#define M_pin 7 // central
#define R_pin 8 // derecho

void setup()
{
    Serial.begin(9600); // Establecer la tasa de baudios a 9600
    pinMode(LED, OUTPUT); // Establecer LED en modo salida
    pinMode(L_pin, INPUT); // Establecer todos los pines de los sensores de seguimiento de línea en modo entrada
    pinMode(M_pin, INPUT);
    pinMode(R_pin, INPUT);
}

void loop ()
{
    int L_val = digitalRead(L_pin); // Leer el valor del sensor izquierdo
    int M_val = digitalRead(M_pin); // Leer el valor del sensor central
    int R_val = digitalRead(R_pin); // Leer el valor del sensor derecho
    Serial.print(L_val);
    Serial.print(" ");
    Serial.print(M_val);
    Serial.print(" ");
    Serial.print(R_val);
    Serial.println(" ");
    delay(100); // Retardo en

    if (L_val == 0 || M_val == 0 || R_val == 0) 
    {
    	digitalWrite(LED, HIGH);
    }
    else 
    {
    	digitalWrite(LED, LOW);
    }
}
```