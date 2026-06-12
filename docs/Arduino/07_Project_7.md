### Proyecto 7: Recepción IR

#### **(1)Descripción:**

![](media/8969111328604c5358f7c915ac94e474.png)

Sin duda, el control remoto infrarrojo es omnipresente en la vida cotidiana. Se utiliza para controlar varios electrodomésticos, como televisores, equipos de sonido, videograbadoras y receptores de señal satelital. El control remoto infrarrojo está compuesto por sistemas de transmisión y recepción infrarroja, es decir, un control remoto infrarrojo, un módulo receptor infrarrojo y un microcontrolador capaz de decodificar.

La señal portadora infrarroja de 38K emitida por el control remoto es codificada por el chip de codificación en el control remoto. Está compuesta por una sección de código piloto, código de usuario, código inverso de usuario, código de datos y código inverso de datos. El intervalo de tiempo del pulso se utiliza para distinguir si es una señal 0 o 1, y la codificación está formada por estas señales 0 y 1.

El código de usuario del mismo control remoto no cambia, mientras que el código de datos puede distinguir la tecla.

Cuando se presiona el botón del control remoto, este envía una señal portadora infrarroja. Cuando el receptor IR recibe la señal, el programa decodificará la señal portadora y determinará qué tecla fue presionada. El MCU decodifica la señal 01 recibida, determinando así qué tecla fue presionada en el control remoto.

![](media/image-20230426172824683.png)

El receptor infrarrojo está soldado en la placa de control del motor. Integra recepción, amplificación y demodulación, cuyo IC interno ya está ajustado para cumplir con la recepción infrarroja y la salida, y es compatible con señales TTL. Emite señales digitales y es adecuado para control remoto infrarrojo y transmisión de datos por infrarrojos. Este módulo solo tiene tres pines, incluyendo señal, VCC y GND, por lo que es muy conveniente conectar y comunicar con microcontroladores como Arduino.

#### **(2)Parámetros:**

Voltaje de operación: 3.3-5V（DC）

Interfaz: 3PIN

Señal de salida: Señal digital

Ángulo de recepción: 90 grados

Frecuencia: 38khz

Distancia de recepción: 10m

Receptor infrarrojo integrado en la placa de control del motor：

![](./media/img-20240117082433.png)




#### **(3)Código de prueba:**

Primero debes importar la librería IR.

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede provocar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 7.1

IRremote

http://www.keyestudio.com

*/

#include <IRremote.h> // declaración de la librería IRremote

int RECV_PIN = 3; // define el pin del receptor IR como 3
IRrecv irrecv(RECV_PIN);
decode_results results; // los resultados de decodificación existen en "result" de "decode results"

void setup() 
{
    Serial.begin(9600);
    irrecv.enableIRIn(); // Habilitar receptor
}

void loop() 
{
    if (irrecv.decode(&results)) // decodificación exitosa, recibe un conjunto de señales infrarrojas
    {
        Serial.println(results.value, HEX); // salida con salto de línea en HEX 16 para recibir el código
        irrecv.resume(); // Recibir el siguiente valor
    }
    delay(100);
}
```

#### **(4)Resultados de la prueba:**

Carga el código de prueba, abre el monitor serial y configura la velocidad de baudios a 9600, apunta el control remoto al receptor IR. Luego se mostrará el valor correspondiente. Si se mantiene presionada una tecla por un momento, aparecerán códigos de error.

![](media/a484b81d031c8d6e8addb169136fd45c.png)

A continuación hemos listado el valor de cada botón del control remoto de Keyestudio. Puedes conservarlo como referencia.

![](media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

El receptor IR está conectado a D3, por lo que no es necesario realizar conexiones adicionales.

#### **(5)Explicación del código:**

**irrecv.enableIRIn():** después de habilitar la decodificación IR, se recibirán las señales IR, luego la función "decode()" verificará continuamente si la decodificación fue exitosa.

**irrecv.decode(&results):** después de decodificar exitosamente, esta función retornará "true" y guardará el resultado en "results". Después de decodificar una señal IR, ejecuta la función resume() y recibe la siguiente señal.

#### **(6)Práctica de extensión:**

Hemos decodificado el valor de tecla del control remoto IR. ¿Qué tal controlar un LED con el valor obtenido? Podríamos diseñar un experimento.

Conecta un LED a D9, luego presiona las teclas del control remoto para encender y apagar el LED.

![](media/e05da7ef9e7b6f63f414f2ca7e3f4ee3.png)

**Código de prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede provocar que la carga falle.)

```C
/*
Keyestudio Mini Tank Robot V3 (Popular Edition)
lesson 7.2
IRremote
http://www.keyestudio.com
*/

#include <IRremote.h> // declaración de IRremote

int RECV_PIN = 3; // define el pin del LED como pin 3
int LED = 9;
bool flag = 0;
IRrecv irrecv(RECV_PIN);
decode_results results; // los resultados de decodificación existen en "result" de "decode results"

void setup() 
{
    Serial.begin(9600);
    pinMode(LED, OUTPUT); // configurar LED como salida
    irrecv.enableIRIn(); // Habilitar receptor
}

void loop() 
{
    if (irrecv.decode(&results)) 
    {
        if (results.value == 0xFF02FD & flag == 0) // El código de tecla anterior, usamos el botón OK del control remoto, si se presiona el botón OK
        {
            digitalWrite(LED, HIGH); // LED encendido
            flag = 1;
        }

        else if (results.value == 0xFF02FD & flag == 1) // presionar nuevamente
        {
            digitalWrite(LED, LOW); // LED apagado
            flag = 0;
        }
        irrecv.resume(); // Recibir el siguiente valor
    }
}
```

Carga el código en la placa de desarrollo y presiona la tecla "OK" del control remoto para encender y apagar el LED.

![](./media/img-20240117090645.png)