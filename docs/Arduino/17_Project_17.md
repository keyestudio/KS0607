### Proyecto 17: Tanque de Control por Bluetooth


#### **(1)Descripción:**

Hemos aprendido los conocimientos básicos sobre Bluetooth en el proyecto anterior. En esta lección, usaremos Bluetooth para controlar el coche inteligente. Dado que involucra Bluetooth, se necesitan un extremo emisor y un extremo receptor. En el proyecto, usamos el teléfono móvil como emisor (maestro), y el coche inteligente conectado con el módulo Bluetooth HM-10 (esclavo) como receptor.

Aprendimos anteriormente que enviar un bit puede controlar los LEDs. Y el principio de controlar este coche robot es el mismo.

Primero entendemos la función de cada botón en la APP, y luego usamos el botón de la APP para controlar el tanque.

#### **(2)Función Principal en la APP**

La siguiente tabla ilustra las funciones de las teclas correspondientes:

|                      TECLAS                       | FUNCIONES                                                    |
| :---------------------------------------------: | ------------------------------------------------------------ |
| ![](media/1118dccd714c7988a51cf2dde58627e3.png) | Emparejar y conectar el módulo Bluetooth HM-10; hacer clic de nuevo para desconectar |
| ![](media/b23e65f788685576275cc16bf0b679cc.png) | seleccionar el robot a operar                                  |
| ![](media/8d910d19cec4d03b5d9cb787425d8d7c.png) | controlar los movimientos del robot mediante botones             |
| ![](media/9c0c7230244e08fc5afa28b18e8b4241.png) | Controlar los movimientos del robot mediante joystick            |
| ![](media/3ab61154b4ae730a3757f40171846825.png) | Controlar los movimientos del robot mediante gravedad             |
| ![](media/fe15b0e4a7e705027cb042d0fd2398ea.png) | Envía "F" cuando se presiona y "S" cuando se suelta<br />El coche avanza cuando se presiona y se detiene cuando se suelta |
| ![](media/b1765938932b8633bd5a96af0293ef24.png) | Envía "L" cuando se presiona y "S" cuando se suelta <br />El coche gira a la izquierda cuando se mantiene presionado y se detiene cuando se suelta |
| ![](media/67f26bd7d2076922470e8805711f2ef9.png) | Envía "R" cuando se presiona y "S" cuando se suelta<br />El coche gira a la derecha cuando se mantiene presionado y se detiene cuando se suelta |
| ![](media/77615a8ca984e538d58e02ac90bc5382.png) | Envía "B" cuando se presiona y "S" cuando se suelta<br />El coche retrocede cuando se mantiene presionado y se detiene cuando se suelta |
| ![](media/f58421773a56c911b09c150d08b0fd67.png) | Envía "u"+dígito+"\#" cuando se arrastra<br />Arrastrar para cambiar la velocidad del motor izquierdo |
| ![](media/a05432839507dd25b7dc7eb1bb9a02bb.png) | Envía "v"+dígito+"\#" cuando se arrastra<br />Arrastrar para cambiar la velocidad del motor derecho |
| ![](media/5dd730ab4d2299210dc2399303b94e33.png) | Seleccionar para entrar a la página de Funciones                                |
| ![](media/a352ca9be952db2838540657b9a70f8c.png) | Envía "G" cuando se presiona y "S" cuando se presiona de nuevo<br />Entra en modo de evitación de obstáculos cuando se presiona y sale cuando se presiona de nuevo |
| ![](media/64da14a6ca501aa97f8eb8895e9f6b1c.png) | Envía "h" cuando se presiona y "S" cuando se presiona de nuevo<br />Entra en modo de seguimiento cuando se presiona y sale cuando se presiona de nuevo |
| ![](media/e4f3b211f8c8b06d1eab9dd2281dff74.png) | Envía "e" cuando se presiona y "S" cuando se presiona de nuevo<br />Entra en modo de seguimiento de línea cuando se presiona y sale cuando se presiona de nuevo |
| ![](media/3d662f37603a8f0c1c34ab2b9ff28c63.png) | Envía "f" cuando se presiona y "S" cuando se presiona de nuevo<br />Entra en modo de movimiento en espacio confinado cuando se presiona y sale cuando se presiona de nuevo |
| ![](media/48ab7c8c488c61abc162dbda0fc75f27.png) | Envía "i" cuando se presiona y "S" cuando se presiona de nuevo<br />Entra en modo de seguimiento de luz cuando se presiona y sale cuando se presiona de nuevo |
| ![](media/4250a152c647cc59f72bf51328943371.png) | Envía "j" cuando se presiona y "S" cuando se presiona de nuevo<br />Entra en modo de extinción de incendios cuando se presiona y sale cuando se presiona de nuevo |
| ![](media/cc420ba3d148bd6b720dd44df9a82768.png) | Seleccionar para entrar en modo de visualización de expresiones faciales               |
| ![](media/17261f134c25702ae129624860ab8fe1.png) | Envía "k" cuando se presiona y "z" cuando se presiona de nuevo<br />Muestra el patrón de sonrisa cuando se hace clic y borra la expresión cuando se hace clic de nuevo |
| ![](media/a8bff045e822a06a24bfd7599c9f142a.png) | Envía "l" cuando se presiona y "z" cuando se presiona de nuevo<br />Muestra el patrón de disgusto cuando se hace clic y borra la expresión cuando se hace clic de nuevo |
| ![](media/8729f3ac4adf446b388221ae2e4cf71f.png) | Envía "m" cuando se presiona y "z" cuando se presiona de nuevo<br />Muestra cara feliz cuando se hace clic y borra la expresión cuando se hace clic de nuevo |
| ![](media/63d935cd1958863f862374ded9b87d6b.png) | Envía "n" cuando se presiona y "z" cuando se presiona de nuevo<br />Muestra el patrón triste cuando se hace clic y borra la expresión cuando se hace clic de nuevo |
| ![](media/5e84087020b919a85495831b231efa5a.png) | Envía "o" cuando se presiona y "z" cuando se presiona de nuevo<br />Muestra el patrón despectivo cuando se hace clic y borra la expresión cuando se hace clic de nuevo |
| ![](media/3b7d99862c2d9a5e7337645b4548091e.png) | Envía "p" cuando se presiona y "z" cuando se presiona de nuevo<br />Muestra el patrón en forma de corazón cuando se hace clic y borra la expresión cuando se hace clic de nuevo |
| ![](media/41bf8b28dea6061cea89b640f5646403.png) | Elegir para entrar en la interfaz de función personalizada; hay seis teclas 1,2,3,4,5,6; con estas teclas, puedes expandir algunas funciones por tu cuenta |
| ![](media/06b8f32aae6c9914ef227d6966ea537f.png) | Clic para enviar "w"<br />Clic para mostrar el valor analógico detectado por la fotorresistencia de la izquierda |
| ![](media/a89df3c223e6a7d4eac29d4fe2ee14af.png) | Clic para enviar "y"<br />Clic para mostrar el valor analógico detectado por la fotorresistencia de la derecha |
| ![](media/a76df707b84409e57a1167889c3510d9.png) | Clic para enviar "x" <br />Clic para mostrar la distancia detectada por el sensor ultrasónico (unidad: cm) |
| ![](media/704e5c6a72d89ee8f78d79ff3cd9537c.png) | Clic para enviar "c", clic de nuevo para enviar "d"<br />Presionar para encender el ventilador y presionar de nuevo para apagarlo |

#### **(3)Diagrama de Flujo:**

![](media/image-20230427101759352.png)

#### **(4)Diagrama de Cableado:**

![](media/930a8024364e07505e845624a94c27bd.png)

El GND, VCC, SDA y SCL de la matriz de puntos LED de 8x16 están conectados respectivamente a -(GND), +(VCC), SDA, SCL de la placa de expansión;

Los pines STATE y BRK del módulo Bluetooth no necesitan ser conectados.

#### **(5)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> Al cargar el código, el módulo Bluetooth debe estar desconectado, y el Bluetooth puede volver a conectarse después del proceso de carga. De lo contrario, es posible que el código no se cargue correctamente.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 17.
  bluetooth Control tank
  http://www.keyestudio.com
*/

// Arreglo, usado para guardar datos de imágenes, puede calcularse por uno mismo u obtenerse de la herramienta de módulo
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
#define SCL_Pin  A5  // Establecer el pin de reloj como A5
#define SDA_Pin  A4  // Establecer el pin de datos como A4

#define ML_Ctrl 4  // Definir el pin de control de dirección del motor izquierdo
#define ML_PWM 6   // Definir el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  // Definir el pin de control de dirección del motor derecho
#define MR_PWM 5   // Definir el pin de control PWM del motor derecho
char ble_val;      // Usado para almacenar el valor obtenido por Bluetooth

void setup() 
{
  Serial.begin(9600);

  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  matrix_display(clear); // limpiar pantallas
  matrix_display(start01);  // mostrar la imagen de inicio
}

void loop() 
{
  if (Serial.available())
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
  }
  switch (ble_val)
  {
    case 'F':  // el comando para avanzar
      Car_front();
      break;
    case 'B':  // el comando para retroceder
      Car_back();
      break;
    case 'L':  // el comando para girar a la izquierda
      Car_left();
      break;
    case 'R':  // el comando para girar a la derecha
      Car_right();
      break;
    case 'S':  // el comando para detenerse
      Car_Stop();
      break;
  }
}

/***************La función para hacer funcionar el motor***************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(back);  // Retroceder
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(front);  // mostrar la imagen de avanzar
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // mostrar la imagen de girar a la izquierda
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // mostrar la imagen de girar a la derecha
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // mostrar la imagen de detenerse
}

// Esta función se usa para la visualización en la pantalla de matriz de puntos
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Función para llamar a la condición de inicio de transferencia de datos
  IIC_send(0xc0);  // Elegir una dirección
  for (int i = 0; i < 16; i++) // Los datos del patrón tienen 16 bytes
  {
    IIC_send(matrix_value[i]); // transferir datos del patrón
  }
  IIC_end();   // Finalizar la transferencia de datos del patrón
  IIC_start();
  IIC_send(0x8A);  // control de visualización, seleccionar ancho de pulso como 4/16
  IIC_end();
}

// Condiciones para el inicio de la transferencia de datos
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

// transferir datos
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) // cada carácter tiene 8 dígitos, que se detectan uno por uno
  {
    if (send_data & mask)  // establecer niveles altos o bajos según cada bit (0 o 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Poner el pin de reloj SCL_Pin en alto para detener la transmisión de datos
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // bajar el pin de reloj SCL_Pin para cambiar las señales de SDA
  }
}
```

#### **(6)Resultado de la Prueba:**

Después de cargar el código, conecte el robot al módulo Bluetooth y empareje la APP de Bluetooth. Encienda el interruptor de alimentación del escudo del controlador de motores. Coloque el robot en el suelo, puede usar estos botones de la app Bluetooth para controlar el robot.

![](media/4655aeffe0d2081fa2b9fd254113c392.jpeg)

1. Las flechas arriba, abajo, izquierda y derecha controlan el robot para que se mueva hacia adelante, hacia atrás, a la izquierda y a la derecha respectivamente.


![](./media/img-20240117095345.png)

2. Haga clic en el botón joystick y jale la dirección del punto negro en el círculo blanco para controlar la dirección de movimiento del robot.

![](./media/img-20240117095401.png)

3. Haga clic en el botón de Gravedad e incline el teléfono en las direcciones hacia adelante, hacia atrás, a la izquierda y a la derecha, y el robot se moverá en la dirección en que se inclina el teléfono.

![](./media/img-20240117095419.png)