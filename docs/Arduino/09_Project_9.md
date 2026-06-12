### Proyecto 9: Matriz de puntos LED de expresión facial 8*16

![](./media/image-20250709110751263.png)

#### **(1)Descripción:**

¿No sería divertido añadir una pantalla de expresiones al robot? La matriz de puntos LED 8*16 de Keyestudio puede lograrlo. Con su ayuda, podrás diseñar expresiones faciales, imágenes, patrones y otros tipos de visualización por ti mismo.

La placa LED 8*16 cuenta con 128 LEDs. Los datos del microprocesador (Arduino) se comunican con el AiP1640 a través de una interfaz de bus de dos hilos. Por lo tanto, puede controlar el encendido y apagado de los 128 LEDs del módulo, de modo que la matriz de puntos del módulo muestre el patrón que necesites. Se proporciona un cable HX-2.54 de 4 pines para mayor comodidad en el cableado.

#### **(2)Parámetros:**

- Voltaje de trabajo: DC 3.3-5V
- Pérdida de potencia: 400mW
- Frecuencia de oscilación: 450KHz
- Corriente de accionamiento: 200mA
- Temperatura de trabajo: -40\~80℃
- Modo de comunicación: bus de dos hilos

#### **(3)Conocimiento:**

**Principio de la matriz de puntos LED 8\*16**

¿Cómo controlar cada LED de la matriz de puntos 8\*16? Se sabe que cada byte tiene 8 bits y cada bit es 0 o 1. Cuando es 0, el LED está apagado, mientras que cuando es 1, el LED está encendido. Un byte puede controlar una columna del LED, y naturalmente 16 bytes pueden controlar 16 columnas de LEDs, eso es la matriz de puntos 8\*16.

![](media/image-20230427082712905.png)

**Descripción de pines y protocolo de comunicación**

Los datos del microprocesador (Arduino) se comunican con el AiP1640 a través de un cable de bus de dos hilos.

El diagrama del protocolo de comunicación es el siguiente: (SCLK) es SCL, (DIN) es SDA

![](media/ea2bab37f23c09453c680590b84653d6.png)

①La condición de inicio para la entrada de datos: SCL está en nivel alto y SDA cambia de alto a bajo.

②Para la configuración del comando de datos, existen métodos como se muestra en la figura a continuación.

En nuestro programa de ejemplo, selecciona la forma de **añadir 1 a la dirección automáticamente**, el valor binario es 0100 0000 y el valor hexadecimal correspondiente es 0x40

![](media/image-20230427083500152.png)

③Para la configuración del comando de dirección, la dirección puede seleccionarse como se muestra a continuación.

El primer 00H está seleccionado en nuestro programa de ejemplo, y el número binario 1100 0000 corresponde al hexadecimal 0xc0

![](media/image-20230427083716284.png)


④El requisito para la entrada de datos es que cuando SCL está en nivel alto al ingresar datos, la señal en SDA debe permanecer sin cambios. Solo cuando la señal de reloj en SCL está en nivel bajo, puede cambiarse la señal en SDA. La entrada de datos es primero el bit menos significativo y luego el bit más significativo.

⑤La condición para el fin de la transmisión de datos es que cuando SCL está en nivel bajo, SDA en nivel bajo y SCL en nivel alto, el nivel de SDA se vuelve alto.

⑥Control de visualización, configurar diferentes anchos de pulso; el ancho de pulso puede seleccionarse como se muestra en la figura a continuación. En el ejemplo, el ancho de pulso es 4/16, y el hexadecimal correspondiente a 1000 1010 es 0x8A

![](media/image-20230427084941994.png)



**Instrucciones para el uso de la herramienta de módulo**

La herramienta de matriz de puntos usa la versión en línea, y el enlace es: [http://dotmatrixtool.com/#]( http://dotmatrixtool.com/#)

①Ingresa al enlace y la página aparece como se muestra a continuación

![](media/354693b5679a2615c62e99b7025d6355.png)

②La matriz de puntos es de 8\*16, así que ajusta la altura a 8 y el ancho a 16, como se muestra en la figura a continuación

![](media/5f0278d66ade370e871b447d360d6e7b.png)

③Genera datos hexadecimales a partir del patrón

Como se muestra en la figura a continuación, presiona el botón izquierdo del ratón para seleccionar, haz clic derecho para cancelar; dibuja el patrón que desees, haz clic en Generate, y se generarán los datos hexadecimales que necesitamos.

![](media/586e88bf13c61b0918046437ed7f6796.png)

#### **(4)Diagrama de conexión:**

![](media/cec50fec4a335b6922e4c6694a133bc1.png)

El GND, VCC, SDA y SCL de la placa de luz LED 8x16 están conectados respectivamente a la placa de expansión de sensores keyestudio -(GND), +(VCC), A4, A5 para comunicación serie de dos hilos.

(<span style="color: rgb(255, 76, 65);">Nota:</span> aunque está conectado con el pin IIC del Arduino, este módulo no es para comunicación IIC. Y el puerto IO aquí es para simular comunicación I2C y puede conectarse con cualquier dos pines)

#### **(5)Código de prueba:**

El código para mostrar la cara sonriente

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.1
  Matrix face
  http://www.keyestudio.com
*/
// obtener los datos de la imagen de sonrisa desde una herramienta de módulo
unsigned char smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};

#define SCL_Pin  A5  // establecer el pin de reloj en A5
#define SDA_Pin  A4  // establecer el pin de datos en A4

void setup() {
  // establecer el pin como SALIDA
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // limpiar pantalla
  //matrix_display(clear);
}
void loop() {
  matrix_display(smile);  // mostrar la imagen de sonrisa
}
// esta función se usa para la visualización de la matriz de puntos
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // usar la función para comenzar a transmitir datos
  IIC_send(0xc0);  // seleccionar una dirección

  for (int i = 0; i < 16; i++) // los datos de imagen tienen 16 caracteres
  {
    IIC_send(matrix_value[i]); // datos para transmitir imágenes
  }

  IIC_end();   // terminar la transmisión de datos de imágenes

  IIC_start();
  IIC_send(0x8A);  // mostrar control y seleccionar ancho de pulso 4/16
  IIC_end();
}

// la condición de inicio de transmisión de datos
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// la señal de fin de transmisión de datos
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// transmitir datos
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // cada carácter tiene 8 dígitos, que se detectan uno por uno
  {
    if (send_data & mask) { // establecer niveles alto o bajo según cada bit (0 o 1)
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // elevar el pin de reloj SCL_Pin para terminar la transmisión de datos
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // bajar el pin de reloj SCL_Pin para cambiar las señales de SDA
  }
}
```

#### **(6)Resultados de la prueba:**

Después de cargar el código de prueba con éxito, conectar según el diagrama de cableado, deslizar el interruptor DIP hacia el extremo derecho y encenderlo, aparece un patrón en forma de sonrisa en la matriz de puntos.

![](media/0fd4831db288e04e75828346ea66a3f5.png)

#### **(7)Proyecto de expansión:**

Usamos la herramienta de módulo que acabamos de aprender, [http://dotmatrixtool.com/#](http://dotmatrixtool.com/#), para hacer que la matriz de puntos muestre el patrón de inicio, avance, parada y luego limpie el patrón. El intervalo de tiempo es de 2000 ms.

![](media/9866c73416df7466b5fe8be3712e6eb3.png)

![](media/1c7ab4b08636c2fe61deaf6c784da7d8.png)

![](media/b0a961f27eb5f0b66603abe23d6bb56a.png)


**Código obtenido de la herramienta de módulo：**

**Código para el patrón de inicio:**

0x01,0x02,0x04,0x08,0x10,0x20,0x40,0x80,0x80,0x40,0x20,0x10,0x08,0x04,0x02,0x01

**Código para el patrón de avance:**

0x00,0x00,0x00,0x00,0x00,0x24,0x12,0x09,0x12,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Código para el patrón de retroceso:**

0x00,0x00,0x00,0x00,0x00,0x24,0x48,0x90,0x48,0x24,0x00,0x00,0x00,0x00,0x00,0x00

**Código para el patrón de giro a la izquierda：**

0x00,0x00,0x00,0x00,0x00,0x00,0x44,0x28,0x10,0x44,0x28,0x10,0x44,0x28,0x10,0x00

**Código para el patrón de giro a la derecha：**

0x00,0x10,0x28,0x44,0x10,0x28,0x44,0x10,0x28,0x44,0x00,0x00,0x00,0x00,0x00,0x00

**Código para el patrón de parada：**

0x2E,0x2A,0x3A,0x00,0x02,0x3E,0x02,0x00,0x3E,0x22,0x3E,0x00,0x3E,0x0A,0x0E,0x00

**Código para limpiar la pantalla：**

0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00

**Código de prueba**


(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conectes el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 9.2
  Matrix face
  http://www.keyestudio.com
*/

// Array, usado para guardar datos de imágenes, puede calcularse usted mismo u obtenerse de la herramienta de módulo
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  // establecer el pin de reloj en A5
#define SDA_Pin  A4  // establecer el pin de datos en A4

void setup() {
  // establecer el pin como SALIDA
  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  // limpiar pantalla
  matrix_display(clear);
}
void loop() {
  matrix_display(start01);  // mostrar imagen "Start"
  delay(2000);
  matrix_display(front);    // mostrar imagen "front"
  delay(2000);
  matrix_display(STOP01);   // mostrar imagen "STOP01"
  delay(2000);
  matrix_display(clear);    // mostrar imagen "clear"
  delay(2000);
}
// esta función se usa para la visualización de la matriz de puntos
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // usar la función para comenzar a transmitir datos
  IIC_send(0xc0);  // seleccionar una dirección

  for (int i = 0; i < 16; i++) // los datos de imagen tienen 16 caracteres
  {
    IIC_send(matrix_value[i]); // datos para transmitir imágenes
  }

  IIC_end();   // terminar la transmisión de datos de imágenes

  IIC_start();
  IIC_send(0x8A);  // mostrar control y seleccionar ancho de pulso 4/16
  IIC_end();
}

// la condición de inicio de transmisión de datos
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

// la señal de fin de transmisión de datos
void IIC_end()
{
  digitalWrite(SCL_Pin, LOW);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, HIGH);
  delayMicroseconds(3);
}

// transmitir datos
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // cada carácter tiene 8 dígitos, que se detectan uno por uno
  {
    if (send_data & mask) { // establecer niveles alto o bajo según cada bit (0 o 1)
      digitalWrite(SDA_Pin, HIGH);
    } else {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // elevar el pin de reloj SCL_Pin para terminar la transmisión de datos
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // bajar el pin de reloj SCL_Pin para cambiar las señales de SDA
  }
}
```

Después de cargar el código de prueba, la placa de expresión facial muestra estos patrones en orden y repite esta secuencia.

![](media/e7ba47508826acc25d348182a0530c05.png)

![](media/831b7e0e07250cbc7bdc4fa509c5a0a3.png)

![](media/dce75583e8bf4bc4377364bf8ed3aa99.png)