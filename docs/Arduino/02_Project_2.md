### Proyecto 2: Ajustar el Brillo del LED

#### **(1) Descripción:**

En la lección anterior, controlamos el encendido y apagado del LED y lo hicimos parpadear.

En este proyecto, controlaremos el brillo del LED mediante PWM simulando un efecto de respiración. Del mismo modo, puedes cambiar el tamaño del paso y el tiempo de retardo en el código para demostrar diferentes efectos de respiración.

PWM es un medio de controlar la salida analógica a través de medios digitales. El control digital se utiliza para generar ondas cuadradas con diferentes ciclos de trabajo (una señal que cambia constantemente entre niveles alto y bajo) para controlar la salida analógica.

En general, los voltajes de entrada de los puertos son 0V y 5V. ¿Qué pasa si se requieren 3V? ¿O un cambio entre 1V, 3V y 3.5V? No podemos cambiar las resistencias constantemente. Por esta razón, recurrimos al PWM.

![](media/bbcfcb9ae56abb7e80ee587246fc4be9.GIF)

Para las salidas de voltaje de los puertos digitales de Arduino, solo hay niveles BAJO y ALTO, que corresponden a las salidas de voltaje de 0V y 5V respectivamente. Puedes definir BAJO como "0" y ALTO como "1", y hacer que Arduino genere quinientos "0" o "1" en 1 segundo. Si genera quinientos "1", eso es 5V; si todos son "0", eso es 0V; si genera un patrón de 250 "01", eso es 2.5V.

Este proceso puede compararse con ver una película. Las películas que vemos no son completamente continuas. En realidad, generan 25 imágenes por segundo, lo cual no puede ser percibido por el ojo humano. Por lo tanto, lo interpretamos como un proceso continuo. El PWM funciona de la misma manera. Para generar diferentes voltajes, necesitamos controlar la proporción de 0 y 1. Cuantos más "0" o "1" se generen por unidad de tiempo, más preciso es el control.

#### **(2) Parámetros:**

![](./media/image-20250709104949184.png)

Interfaz de control: Puerto digital 3

Voltaje de trabajo: DC 3.3-5V

Espaciado entre pines: 2.54mm

Color de visualización del LED: amarillo

#### **(3) Diagrama de Conexión:**

Los pines PWM de Arduino están conectados a 3, 5, 6, 9, 10 y 11. Mantén el pin 9 sin cambios.

![](media/8ad54723c1d6149952c730217a1861cd.png)

#### **(4) Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.1

pwm

http://www.keyestudio.com

*/

int LED = 9; // Define el pin del LED como 9

void setup () 
{
	pinMode(LED, OUTPUT); // Configura el pin del LED como SALIDA
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED ENCENDIDO
		delay(5); // retardo de 5ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // El LED se atenúa
		delay(5); // retardo de 5ms
	}
}
```

#### **(5) Resultados de la Prueba:**

Al cargar el código de prueba exitosamente, el LED cambia gradualmente de brillante a oscuro, como la respiración humana, en lugar de encenderse y apagarse inmediatamente.

#### **(6) Explicación del Código:**

Para repetir ciertas instrucciones, podemos usar la sentencia FOR. El formato de la sentencia FOR se muestra a continuación:

![图1(1)](media/65da124bdd0ea488291c71c6b879fe95.jpeg)

Secuencia cíclica del FOR:

Ronda 1: 1 → 2 → 3 → 4

Ronda 2: 2 → 3 → 4

…

Hasta que el número 2 no se cumpla, el ciclo "for" termina.

Después de conocer este orden, volvamos al código:

**for (int value = 0; value \< 255; value=value+1){**

**...}**

**for (int value = 255; value \>0; value=value-1){**

**...}**

Las dos sentencias "for" hacen que el valor aumente de 0 a 255, luego disminuya de 255 a 0, luego aumente a 255, .... en un bucle infinito.

Hay una nueva función a continuación ----- analogWrite()

Sabemos que el puerto digital solo tiene dos estados, 0 y 1. Entonces, ¿cómo se envía un valor analógico a un valor digital? Aquí es donde se necesita esta función. Observemos la placa Arduino y encontremos 6 pines marcados con "\~" que pueden generar señales PWM.

El formato de la función es el siguiente:

**analogWrite(pin,value)**

analogWrite() se utiliza para escribir un valor analógico de 0 a 255 en un puerto PWM, por lo que el valor está en el rango de 0 a 255. Ten en cuenta que solo puedes escribir en los pines digitales con función PWM, como los pines 3, 5, 6, 9, 10, 11.

PWM es una tecnología para obtener una cantidad analógica mediante métodos digitales. El control digital forma una onda cuadrada, y la señal de onda cuadrada solo tiene dos estados de encendido y apagado (es decir, niveles alto o bajo). Al controlar la proporción de la duración del encendido y apagado, se puede simular un voltaje que varía de 0 a 5V. El tiempo de encendido (académicamente denominado nivel alto) se llama ancho de pulso, por lo que PWM también se denomina modulación por ancho de pulso.

A través de las siguientes cinco ondas cuadradas, conozcamos más sobre el PWM.

![](media/553f3d1b6ca04e1aa0479841dd075fa2.png)

En la figura anterior, la línea verde representa un período, y el valor de analogWrite() corresponde a un porcentaje que también se denomina Ciclo de Trabajo.

El ciclo de trabajo implica que la duración del nivel alto se divide por la duración del nivel bajo en un ciclo. De arriba hacia abajo, el ciclo de trabajo de la primera onda cuadrada es 0% y su valor correspondiente es 0. El brillo del LED es el más bajo, es decir, apagado. Cuanto más tiempo dure el nivel alto, más brillante será el LED. Por lo tanto, el último ciclo de trabajo es 100%, que corresponde a 255, y el LED es el más brillante. Y 25% significa más oscuro.

El PWM se usa principalmente para ajustar el brillo del LED o la velocidad de rotación de los motores.

Juega un papel vital en el control de robots con ruedas inteligentes. Creo que no puedes esperar para aprender el siguiente proyecto.

#### **(7) Práctica de Extensión:**

Modifiquemos el valor del retardo y mantengamos el pin sin cambios, luego observemos cómo cambia el LED.

**Código de Prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 2.2

pwm-slow

http://www.keyestudio.com

*/

int LED = 9; // Define el pin del LED como 9

void setup() 
{
	pinMode(LED, OUTPUT); // Configura el pin del LED como SALIDA
}

void loop () 
{
	for (int value = 0; value < 255; value = value + 1) 
    {
		analogWrite(LED, value); // LED ENCENDIDO
		delay(30); // retardo de 30ms
	}
	for (int value = 255; value > 0; value = value - 1) 
    {
		analogWrite(LED, value); // El LED se atenúa
		delay (30); // retardo de 30ms
	}
}
```

Carga el código en la placa de desarrollo y el LED parpadeará más lentamente.