### Proyecto 1: Parpadeo de LED

#### **(1)Descripción:**

![](media/64b0b431d58473408ac46b39d2dc2ad0.jpeg)

![](media/ae87aea86f6c7e427f7adfc0e7c0efe3.png)

Para principiantes y entusiastas, el parpadeo de LED es un programa fundamental. LED, la abreviatura de diodos emisores de luz, está compuesto por compuestos químicos de Ga, As, P, N, entre otros. El LED puede parpadear en diversos colores modificando el tiempo de retardo en el código de prueba. Durante el control, se alimenta GND y VCC. El LED se encenderá si el extremo S está en nivel alto; de lo contrario, se apagará.

#### **(2)Parámetros:**

![](./media/image-20250709104606457.png)

- Interfaz de control: puerto digital
- Voltaje de trabajo: DC 3.3-5V
- Espaciado de pines: 2.54mm
- Color de visualización del LED: amarillo

#### **(3)Componentes Requeridos:**

![](media/img-20240117081416.png)


#### **(4)Placa de expansión del motor 8833:**

La placa de expansión del motor Keyestudio 8833 es compatible con la placa de desarrollo Arduino UNO. Solo apílela sobre la placa de desarrollo al utilizarla.

![](./media/image-20250709104749140.png)

#### **(5)Diagrama de Conexión:**

![](media/8ad54723c1d6149952c730217a1861cd.png)

![](media/d68e6475a7c9ed55bb057b75d1b11689.png)

<span style="color: rgb(255, 76, 65);">**NOTA:**</span> El LED está conectado al puerto D9. Recuerde instalar los puentes (jumper caps) en el shield.

#### **(6)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede provocar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.1

Blink

http://www.keyestudio.com

*/

int LED = 9; // Define el pin del LED para conectar con el puerto digital 9

void setup()
{
	pinMode(LED, OUTPUT); // Inicializa el pin del LED en modo de salida
}

void loop() // Bucle infinito
{
	digitalWrite(LED, HIGH); // Salida de nivel alto y enciende el LED
	delay(1000); // Espera 1s
	digitalWrite(LED, LOW); // Salida de nivel bajo y apaga el LED
	delay(1000); // Espera 1s
}
```

#### **(7)Resultados de la Prueba:**

Cargue el programa, el LED parpadea con un intervalo de 1s.

#### **(8)Explicación del Código:**

**pinMode(LED，OUTPUT) -** Esta función puede indicar que el pin es de ENTRADA (INPUT) o SALIDA (OUTPUT)

**digitalWrite(LED，HIGH) -** Cuando el pin está en modo OUTPUT, podemos configurarlo en HIGH (salida de 5V) o LOW (salida de 0V)

#### **(9)Práctica de Extensión:**

Hemos logrado hacer parpadear el LED. A continuación, observemos qué le sucederá al LED si modificamos los pines y el tiempo de retardo.

**Código de Prueba**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede provocar que la carga falle.)

```C
/*

Keyestudio Mini Tank Robot V3 (Popular Edition)

lesson 1.2

Blink

http://www.keyestudio.com

*/

int LED = 9; // Define el pin del LED como 9

void setup()
{
	pinMode(LED, OUTPUT); // Configura el pin del LED como OUTPUT
}

void loop() // Bucle infinito
{
    digitalWrite(LED, HIGH); // Salida de niveles altos, enciende el LED
	delay(100); // Espera 0.1s
	digitalWrite(LED, LOW); // Salida de niveles bajos del LED, apaga el LED
	delay(100); // Espera 0.1s

}
```

El resultado de la prueba muestra que el LED parpadea más rápido. Por lo tanto, podemos concluir que los pines y el tiempo de retardo afectan la frecuencia de parpadeo.