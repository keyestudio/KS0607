### Proyecto 15: Tanque con Control Remoto IR

![](./media/image-20250709113214889.png)


#### **(1)Descripción:**

El control remoto infrarrojo es uno de los controles remotos más comunes que se encuentran en aplicaciones como motores eléctricos, ventiladores eléctricos y muchos otros electrodomésticos. En este proyecto, utilizamos los conocimientos que aprendimos anteriormente para fabricar un coche inteligente controlado por infrarrojos.

En la lección 9, hemos probado el valor de tecla correspondiente a cada botón del control remoto infrarrojo. En el proyecto, podemos establecer el código (valor de tecla) para que el botón correspondiente controle los movimientos del coche inteligente y muestre los patrones de movimiento en la matriz de LED 8X16.

La lógica específica del coche inteligente con control remoto infrarrojo se muestra en la tabla:

|                        Tecla ultrasónica                        | Valor de tecla |                    Instrucciones de las teclas                    |
| :----------------------------------------------------------: | :-------: | :----------------------------------------------------------: |
| ![image-20230427094710725](media/image-20230427094710725.png) |  FF629D   | Avanzar（establecer PWM en 200）<br />mostrar el patrón de avance |
| ![image-20230427094716639](media/image-20230427094716639.png) |  FFA857   | Retroceder（establecer PWM en 200）<br />mostrar el patrón de retroceso |
| ![image-20230427094720417](media/image-20230427094720417.png) |  FF22DD   |           Girar a la izquierda<br />mostrar el patrón "STOP"           |
| ![image-20230427094725151](media/image-20230427094725151.png) |  FFC23D   |     Girar a la derecha<br />mostrar el patrón de giro a la izquierda      |
| ![image-20230427094729839](media/image-20230427094729839.png) |  FF02FD   |             Detener<br />mostrar el patrón "STOP"              |

**Configuración inicial**: La matriz de LED 8X16 muestra el patrón "![](media/wps20.jpg)".



#### **(2)Diagrama de flujo:**

![](media/wps21.png)

#### **(3)Diagrama de conexión:**

![](media/54527fe245b218dd22bdff5dafd4805d.png)

<span style="color: rgb(255, 76, 65);">Nota:</span>

GND, VCC, SDA y SCL del panel LED 8x16 están conectados a G（GND), V（VCC), SDA y SCL de la placa de expansión.

Dado que la placa 8833 integra el receptor IR, no es necesario cablearla. Los pines del receptor IR son G（GND), V（VCC) y D3.

#### (4)**Código de prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, ya que la carga del código también utiliza comunicación serial y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar un fallo en la carga.)

```C
/*
 Keyestudio Mini Tank Robot V3 (Popular Edition)
 lesson 15
 IRremote Control Tank
 http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  // Se usa para almacenar los valores infrarrojos recibidos

// Array, utilizado para guardar datos de imágenes, puede calcularse manualmente u obtenerse con la herramienta de módulo
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
#define MR_PWM 5    // Definir el pin de control PWM del motor derecho

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  // Inicializar la biblioteca del receptor infrarrojo

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
  if (irrecv.decode(&results))  // Recibir valor del control remoto infrarrojo
  {
    ir_rec = results.value;
    String type = "UNKNOWN";
    String typelist[14] = {"UNKNOWN", "NEC", "SONY", "RC5", "RC6", "DISH", "SHARP", "PANASONIC", "JVC", "SANYO", "MITSUBISHI", "SAMSUNG", "LG", "WHYNTER"};
    if (results.decode_type >= 1 && results.decode_type <= 13) 
    {
      type = typelist[results.decode_type];
    }
    Serial.print("IR TYPE:" + type + "  ");
    Serial.println(ir_rec, HEX);
    irrecv.resume();
  }

  switch (ir_rec) 
  {
    case 0xFF629D: Car_front();     break;   // comando para avanzar
    case 0xFFA857: Car_back();      break;   // comando para retroceder
    case 0xFF22DD: Car_T_left();    break;   // comando para girar a la izquierda
    case 0xFFC23D: Car_T_right();   break;   // comando para girar a la derecha
    case 0xFF02FD: Car_Stop();      break;   // comando para detenerse
    case 0xFF30CF: Car_left();      break;   // comando para rotar a la izquierda
    case 0xFF7A85: Car_right();     break;   // comando para rotar a la derecha
    default: break;
  }
}

/***************Función para hacer funcionar el motor***************/
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
  matrix_display(front);  // mostrar la imagen de avance
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
  matrix_display(left);  // mostrar la imagen de giro a la izquierda
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
  matrix_display(right);  // mostrar la imagen de giro a la derecha
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  // mostrar la imagen de parada
}

void Car_T_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 100);
  matrix_display(left);  // mostrar la imagen de giro a la izquierda
}

void Car_T_right() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 100);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 0);
  matrix_display(right);  // mostrar la imagen de giro a la derecha
}

// Esta función se utiliza para la visualización en la pantalla de matriz de puntos
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
    if (send_data & mask)  // establecer niveles alto o bajo según cada bit (0 o 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); // Llevar el pin de reloj SCL_Pin a alto para detener la transmisión de datos
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); // bajar el pin de reloj SCL_Pin para cambiar las señales de SDA
  }
}
```

#### **(5)Resultado de la prueba:**

Después de cargar el código, encienda el interruptor de alimentación del escudo del motor. Coloque el robot en el suelo, consulte la tabla anterior y presione diferentes botones; el robot se moverá en la dirección preestablecida correspondiente.

![](./media/img-20240117090114.png)