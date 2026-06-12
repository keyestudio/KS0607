### Proyecto 18: Robot con Control de Velocidad por BT

#### (1)**Descripción:**

En el proyecto anterior, aprendimos cómo controlar el tanque inteligente con Bluetooth. El valor PWM del motor que usamos anteriormente es 200 (la velocidad es 200).

En esta lección, usaremos Bluetooth para ajustar la velocidad del carro inteligente. No está limitado a una velocidad fija de 200. Definimos dos variables para almacenar los valores de velocidad de los motores izquierdo y derecho respectivamente. A través del estudio previo, sabemos que el rango de este valor solo puede tomar de 0 a 255.

#### **(2)Diagrama de flujo:**

![](media/image-20230427102042028.png)

#### **(3)Diagrama de conexión:**

![](media/930a8024364e07505e845624a94c27bd.png)

El GND, VCC, SDA y SCL de la matriz de LED 8x16 están conectados respectivamente a -(GND), +(VCC), SDA, SCL de la placa de expansión;

#### **(4)Código de prueba:**

(<span style="color: rgb(255, 76, 65);">Nota:</span> Al cargar el código, el módulo Bluetooth debe estar desconectado, y el Bluetooth puede volver a conectarse después del proceso de carga. De lo contrario, es posible que el código no se grabe.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 18
  bluetooth control speed tank
  http://www.keyestudio.com
*/

// Array, usado para guardar datos de imágenes, puede calcularse manualmente o obtenerse de la herramienta de módulo
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char speed_a[] = {0x00, 0x00, 0x00, 0x20, 0x10, 0x08, 0x04, 0x02, 0xff, 0x02, 0x04, 0x08, 0x10, 0x20, 0x00, 0x00};
unsigned char speed_d[] = {0x00, 0x00, 0x00, 0x04, 0x08, 0x10, 0x20, 0x40, 0xff, 0x40, 0x20, 0x10, 0x08, 0x04, 0x00, 0x00};
#define SCL_Pin  A5  // establecer el pin del reloj en A5
#define SDA_Pin  A4  // establecer el pin de datos en A4

#define ML_Ctrl 4  // definir el pin de control de dirección del motor izquierdo
#define ML_PWM 6   // definir los pines de control PWM del motor izquierdo
#define MR_Ctrl 2  // definir el pin de control de dirección del motor derecho
#define MR_PWM 5   // definir el pin de control PWM del motor derecho
char ble_val;      // definir el pin de control PWM del motor derecho
byte speeds_L = 200; // La velocidad inicial del motor izquierdo es 200
byte speeds_R = 200; // La velocidad inicial del motor derecho es 200
String speeds_l, speeds_r; // Recibir una cadena de PWM para convertirla a un valor entero de PWM

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
  if (Serial.available() > 0) 
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F':  // el comando para ir hacia adelante
        Car_front();
        break;
      case 'B':  // el comando para ir hacia atrás
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
      case 'u':  // Recibir una cadena que comienza con u y termina con #, y convertirla a un valor entero
        speeds_l = Serial.readStringUntil('#');
        speeds_L = String(speeds_l).toInt();
        break;
      case 'v':  // Recibir una cadena que comienza con v y termina con #, y convertirla a un valor entero
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt();
        break;
    }
  }
}

/***************La función para hacer funcionar el motor***************/

void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  // Ir hacia atrás
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  // mostrar la imagen de ir hacia adelante
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  // mostrar la imagen de girar a la izquierda
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  // mostrar la imagen de girar a la derecha
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // mostrar la imagen de parada
}

// Esta función se usa para la visualización en la pantalla de matriz de puntos
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  // Función para llamar la condición de inicio de transferencia de datos
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
    digitalWrite(SCL_Pin, HIGH); // Subir el pin de reloj SCL_Pin a nivel alto para detener la transmisión de datos
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // bajar el pin de reloj SCL_Pin para cambiar las señales de SDA
  }
}
```

#### **(5)Resultados de la prueba:**

Después de cargar el código de prueba correctamente, deslizar el interruptor DIP hacia el extremo derecho, encenderlo y emparejar la APP con Bluetooth, el carro inteligente puede ser controlado para moverse mediante la APP. Y la velocidad del carro puede regularse moviendo los controles deslizantes de velocidad de los motores izquierdo y derecho.

![](media/b9c902b937801f829b9ce2fd254b1849.jpeg)

(Puede consultar la tabla de funciones en el proyecto 17)