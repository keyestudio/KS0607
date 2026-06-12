### Proyecto 23: Múltiples Funciones del Robot Extintor de Incendios


#### **(1)Descripción:**

El auto inteligente ha realizado una función individual en cada proyecto anterior.

¿Puede mostrar múltiples funciones al mismo tiempo? Sí.

En este último gran proyecto, tenemos la intención de usar un código completo para controlar el auto inteligente y mostrar todas las funciones mencionadas en proyectos anteriores. Usamos las teclas de la APP Bluetooth para cambiar automáticamente entre varias funciones, muy simple y conveniente.



#### **(2)Diagrama de Flujo:**

<span style="color: rgb(255, 76, 65);">**Por favor, consulte el Proyecto 16 para instalar y configurar la APP Bluetooth**</span>

![](media/image-20230427102547633.png)

#### **(3)Diagrama de Conexión:**

![](media/e7ac834ba04aa2e8862995d2d33ce9356.jpg)

1\. GND, VCC, SDA y SCL de la placa 8x16 están conectados a G (GND), + (VCC), A4 y A5 de la placa de expansión.

2\. VCC, IN+, IN- y Gnd del módulo del ventilador están conectados a 5V (V), 12 (S), 13 (S) y Gnd (G).

3\. El cable marrón, el cable rojo y el cable naranja del servo están conectados a Gnd (G), 5v (V) y D10.

4\. RXD, TXD, GND y VCC del módulo BT están conectados a TX, RX, G (GND) y 5V (VCC). STATE y BRK no necesitan ser conectados.

5\. Los pines "G", "V" y A del sensor de llama izquierdo están conectados a G (GND), V (VCC) y A1, respectivamente; El sensor de llama derecho está conectado a G (GND), V (VCC) y A2, respectivamente.

6\. Los puertos distales del sensor de seguimiento de línea son 11, 7 y 8.

#### **(4)Código de Prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 23
  Fire Extinguishing Robot Multiple Functions
  http://www.keyestudio.com
*/
#include <IRremote.h>
IRrecv irrecv(3);  //
decode_results results;
long ir_rec;  //usado para guardar el valor IR 

/***********/
#define USE_FAN_FUNCTION   1

//Array, usado para guardar datos de imágenes, puede calcularse por uno mismo u obtenerse de la herramienta de módulo
unsigned char start01[] = {0x01, 0x02, 0x04, 0x08, 0x10, 0x20, 0x40, 0x80, 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01};
unsigned char STOP01[] = {0x2E, 0x2A, 0x3A, 0x00, 0x02, 0x3E, 0x02, 0x00, 0x3E, 0x22, 0x3E, 0x00, 0x3E, 0x0A, 0x0E, 0x00};
unsigned char front[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x12, 0x09, 0x12, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char back[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x24, 0x48, 0x90, 0x48, 0x24, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};
unsigned char left[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x44, 0x28, 0x10, 0x00};
unsigned char right[] = {0x00, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x10, 0x28, 0x44, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

unsigned char Smile[] = {0x00, 0x00, 0x1c, 0x02, 0x02, 0x02, 0x5c, 0x40, 0x40, 0x5c, 0x02, 0x02, 0x02, 0x1c, 0x00, 0x00};
unsigned char Disgust[] = {0x00, 0x00, 0x02, 0x02, 0x02, 0x12, 0x08, 0x04, 0x08, 0x12, 0x22, 0x02, 0x02, 0x00, 0x00, 0x00};
unsigned char Happy[] = {0x02, 0x02, 0x02, 0x02, 0x08, 0x18, 0x28, 0x48, 0x28, 0x18, 0x08, 0x02, 0x02, 0x02, 0x02, 0x00};
unsigned char Squint[] = {0x00, 0x00, 0x00, 0x41, 0x22, 0x14, 0x48, 0x40, 0x40, 0x48, 0x14, 0x22, 0x41, 0x00, 0x00, 0x00};
unsigned char Despise[] = {0x00, 0x00, 0x06, 0x04, 0x04, 0x04, 0x24, 0x20, 0x20, 0x26, 0x04, 0x04, 0x04, 0x04, 0x00, 0x00};
unsigned char Heart[] = {0x00, 0x00, 0x0C, 0x1E, 0x3F, 0x7F, 0xFE, 0xFC, 0xFE, 0x7F, 0x3F, 0x1E, 0x0C, 0x00, 0x00, 0x00};

unsigned char clear[] = {0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00};

#define SCL_Pin  A5  //establecer el pin del reloj en A5
#define SDA_Pin  A4  //establecer el pin de datos en A4

#define ML_Ctrl 4  //definir el pin de control de dirección del motor izquierdo como 4
#define ML_PWM 6   //definir el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  //definir el pin de control de dirección del sensor derecho
#define MR_PWM 5   //definir el pin de control PWM del motor derecho
char ble_val;      //usado para guardar el valor Bluetooth
byte speeds_L = 200; //la velocidad inicial del motor izquierdo es 200
byte speeds_R = 200; //la velocidad inicial del motor derecho es 200
String speeds_l, speeds_r; //recibir caracteres PWM y convertirlos en valor PWM

//conectar el sensor de seguimiento de línea
#define L_pin  11  //izquierda
#define M_pin  7  //centro
#define R_pin  8  //derecha
int L_val, M_val, R_val;

#if USE_FAN_FUNCTION  /****usar ventilador*******/
int flame_L = A1; //definir el puerto analógico del sensor de llama izquierdo en A1
int flame_R = A2; //definir el puerto analógico del sensor de llama derecho en A2
int flame_valL, flame_valR;

//el pin del motor 130
int INA = 12;
int INB = 13;

#else /****usar el sensor ultrasónico*******/
#define servoPin    10  //pin del servo
#define light_L_Pin A1   //definir el pin de la fotoresistencia izquierda
#define light_R_Pin A2   //definir el pin de la fotoresistencia derecha
int left_light;
int right_light;

#define Trig 12
#define Echo 13
float distance;//Almacenar los valores de distancia detectados por el ultrasónico para seguimiento

//Almacenar los valores de distancia detectados por el ultrasónico para evitar obstáculos
int a;
int a1;
int a2;

#endif

bool flag;  //variable de bandera, usada para entrar y salir de un modo

void setup() 
{
  Serial.begin(9600);
  irrecv.enableIRIn();  //Inicializar la librería del control remoto IR

  pinMode(SCL_Pin, OUTPUT);
  pinMode(SDA_Pin, OUTPUT);
  
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);

  pinMode(L_pin, INPUT); //definir los pines de los sensores como ENTRADA
  pinMode(M_pin, INPUT);
  pinMode(R_pin, INPUT);

  matrix_display(clear);    //limpiar pantalla
  matrix_display(start01);  //mostrar inicio

#if USE_FAN_FUNCTION/****usar el ventilador*******/
  pinMode(INA, OUTPUT);//establecer INA como SALIDA
  pinMode(INB, OUTPUT);//establecer INB como SALIDA

  //definir entradas del sensor de llama
  pinMode(flame_L, INPUT);
  pinMode(flame_R, INPUT);
#else/****usar el sensor ultrasónico*******/
  pinMode(servoPin, OUTPUT);
  pinMode(light_L_Pin, INPUT);
  pinMode(light_R_Pin, INPUT);

  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  procedure(90); //establecer el ángulo del servo en 90°
#endif
}

void loop() 
{
  if (Serial.available()) //si hay datos en el buffer serial
  {
    ble_val = Serial.read();
    Serial.println(ble_val);
    switch (ble_val) 
    {
      case 'F': Car_front(); break; //el comando para ir hacia adelante

      case 'B': Car_back(); break;  //el comando para ir hacia atrás

      case 'L': Car_left(); break;  //el comando para girar a la izquierda

      case 'R': Car_right(); break; //el comando para girar a la derecha

      case 'S': Car_Stop();  break; //detener

      case 'e': Tracking();  break; //entrar al modo de seguimiento de línea

      case 'f': Confinement(); break;  //entrar al modo de confinamiento

#if USE_FAN_FUNCTION/****usar ventilador*******/
      case 'j': Fire(); break;  //activar el modo de extinción de incendios

      case 'c': fan_begin(); break;  //activar el ventilador

      case 'd': fan_stop();  break;  //apagar el ventilador

#else/****usar el sensor ultrasónico*******/
      case 'g': Avoid(); break;  //entrar al modo de evitación de obstáculos

      case 'h': Follow(); break;  //entrar al modo de seguimiento

      case 'i': Light_following();  break;  //entrar al modo de seguimiento de luz
#endif
      case 'u': 
        speeds_l = Serial.readStringUntil('#'); 
        speeds_L = String(speeds_l).toInt(); 
        break; //comenzar recibiendo u, terminar recibiendo el carácter # y convertir en entero

      case 'v': 
        speeds_r = Serial.readStringUntil('#');
        speeds_R = String(speeds_r).toInt(); 
        break; //comenzar recibiendo u, terminar recibiendo el carácter # y convertir en entero

      case 'k': matrix_display(Smile);    break;  //mostrar cara "sonriente"
      case 'l': matrix_display(Disgust);  break;  //mostrar cara "disgustada"
      case 'm': matrix_display(Happy);    break;  //mostrar cara "feliz"
      case 'n': matrix_display(Squint);   break;  //mostrar cara "triste"
      case 'o': matrix_display(Despise);  break;  //mostrar cara "despreciativa"
      case 'p': matrix_display(Heart);    break;  //mostrar la imagen del corazón
      case 'z': matrix_display(clear);    break;  //limpiar imágenes

      default: break;
    }
  }

#if (USE_FAN_FUNCTION != 1)/****la función para no usar el ventilador*******/
  //Las siguientes tres señales se usan principalmente para impresión cíclica
  if (ble_val == 'x') 
  {
    distance = checkdistance(); Serial.println(distance);
    delay(50);
  } 
  else if (ble_val == 'w') 
  {
    left_light = analogRead(light_L_Pin);
    Serial.println(left_light);
    delay(50);
  } 
  else if (ble_val == 'y') 
  {
    right_light = analogRead(light_R_Pin);
    Serial.println(right_light);
    delay(50);
  }
#endif

  if (irrecv.decode(&results))  //Recibir valor del control remoto infrarrojo
  {
    ir_rec = results.value;
    Serial.println(ir_rec, HEX);
    switch (ir_rec) 
    {
      case 0xFF629D: Car_front();   break;   //ir hacia adelante
      case 0xFFA857: Car_back();    break;   //ir hacia atrás
      case 0xFF22DD: Car_left();    break;   //girar a la izquierda
      case 0xFFC23D: Car_right();   break;   //girar a la derecha
      case 0xFF02FD: Car_Stop();    break;   //detener
      default: break;
    }
    irrecv.resume();
  }
}

#if (USE_FAN_FUNCTION != 1)/****usar el sensor ultrasónico*******/

//Controlar el sensor ultrasónico
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //
  delay(10);
  return distance;
}


//la función para controlar el servo
void procedure(int myangle) 
{
  int pulsewidth;
  pulsewidth = map(myangle, 0, 180, 500, 2000);  //Calcular el valor del ancho de pulso, que debe ser el valor de mapeo de 500 a 2500. Considerando la influencia de la librería infrarroja, se usa 500~2000 aquí.
  for (int i = 0; i < 5; i++) 
  {
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //La duración del nivel alto es el ancho de pulso
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //El período es 20ms, por lo que el nivel bajo dura el resto del tiempo
  }
}

/*****************evitación de obstáculos******************/
void Avoid()
{
  flag = 0;
  while (flag == 0)
  {
    a = checkdistance();  //la distancia frontal se establece en a
    if (a < 20) //Cuando la distancia al frente es menor a 20cm
    {
      Car_Stop();  //detener
      delay(500); //retardo de 500ms
      procedure(180);  //el servo gira a la izquierda
      delay(500); //retardo de 500ms
      a1 = checkdistance();  //la distancia izquierda se establece en a1
      delay(100); //leer valor

      procedure(0); //el servo gira a la derecha
      delay(500); //retardo de 500ms
      a2 = checkdistance(); ///la distancia derecha se establece en a2
      delay(100); //leer valor

      procedure(90);  //volver a 90°
      delay(500);
      if (a1 > a2)  //Cuando la distancia a la izquierda es mayor que la distancia a la derecha
      {
        Car_left();  //el robot gira a la izquierda
        delay(700);  //girar a la izquierda 700ms
      } 
      else 
      {
        Car_right(); //girar a la derecha
        delay(700);
      }
    }
    else  //si la distancia frontal ≥20cm, el robot avanza
    {
      Car_front(); //avanzar
    }
    //recibir el valor Bluetooth para salir del bucle
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')  //recibir S
      {
        flag = 1;  //establecer flag en 1 para salir del bucle
        Car_Stop();
      }
    }
  }
}

/*******************seguimiento***************/
void Follow() 
{
  flag = 0;
  while (flag == 0) 
  {
    distance = checkdistance();  //establecer el valor de distancia en distance
    if (distance >= 20 && distance <= 60) //avanzar
    {
      Car_front();
    }
    else if (distance > 10 && distance < 20)  // detener
    {
      Car_Stop();
    }
    else if (distance <= 10)  //retroceder
    {
      Car_back();
    }
    else  //detener
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S')
      {
        flag = 1;  //salir del bucle
        Car_Stop();
      }
    }
  }
}

/****************seguimiento de luz******************/
void Light_following() 
{
  flag = 0;
  while (flag == 0) 
  {
    left_light = analogRead(light_L_Pin);
    right_light = analogRead(light_R_Pin);
    if (left_light > 650 && right_light > 650) //avanzar
    {
      Car_front();
    }
    else if (left_light > 650 && right_light <= 650)  //girar a la izquierda
    {
      Car_left();
    }
    else if (left_light <= 650 && right_light > 650) //girar a la derecha
    {
      Car_right();
    }
    else  //de lo contrario, detener
    {
      Car_Stop();
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#else/****usar el ventilador*******/
/***************activar el ventilador*****************/
void fan_begin() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, HIGH);
}

/***************detener el ventilador*****************/
void fan_stop() 
{
  digitalWrite(INA, LOW);
  digitalWrite(INB, LOW);
}

/***************extinguir incendio****************/
void Fire() 
{
  flag = 0;
  while (flag == 0) 
  {
    //Leer el valor analógico del sensor de llama
    flame_valL = analogRead(flame_L);
    flame_valR = analogRead(flame_R);
    if (flame_valL <= 700 || flame_valR <= 700) 
    {
      Car_Stop();
      fan_begin();
    } 
    else 
    {
      fan_stop();
      L_val = digitalRead(L_pin); //Leer el valor del sensor izquierdo
      M_val = digitalRead(M_pin); //Leer el valor del sensor central
      R_val = digitalRead(R_pin); //Leer el valor del sensor derecho
```

```
     if (M_val == 1)  //el del medio detecta líneas negras
      {
        if (L_val == 1 && R_val == 0)  //Si se detecta una línea negra a la izquierda, pero no a la derecha, girar a la izquierda
        {
          Car_left();
        }
        else if (L_val == 0 && R_val == 1)  //Si se detecta una línea negra a la derecha, no a la izquierda, girar a la derecha
        {
          Car_right();
        }
        else //avanzar
        { 
          Car_front();
        }
      }
      else //el del medio detecta líneas negras
      { 
        if (L_val == 1 && R_val == 0) //Si se detecta una línea negra a la izquierda, pero no a la derecha, girar a la izquierda
        { 
          Car_left();
        }
        else if (L_val == 0 && R_val == 1) //Si se detecta una línea negra a la derecha, no a la izquierda, girar a la derecha
        { 
          Car_right();
        }
        else //de lo contrario detener
        { 
          Car_Stop();
        }
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

#endif

/***************seguimiento de línea*****************/
void Tracking() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //Leer el valor del sensor izquierdo
    M_val = digitalRead(M_pin); //Leer el valor del sensor intermedio
    R_val = digitalRead(R_pin); //Leer el valor del sensor derecho
    if (M_val == 1)  //el del medio detecta líneas negras
    {
      if (L_val == 1 && R_val == 0) //Si se detecta una línea negra a la izquierda, pero no a la derecha, girar a la izquierda
      {
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //Si se detecta una línea negra a la derecha, no a la izquierda, girar a la derecha
      { 
        Car_right();
      }
      else //avanzar
      { 
        Car_front();
      }
    }
    else //el sensor del medio no detecta líneas negras
    { 
      if (L_val == 1 && R_val == 0) //Si se detecta una línea negra a la izquierda, pero no a la derecha, girar a la izquierda
      { 
        Car_left();
      }
      else if (L_val == 0 && R_val == 1) //Si se detecta una línea negra a la derecha, no a la izquierda, girar a la derecha
      { 
        Car_right();
      }
      else //de lo contrario detener
      { 
        Car_Stop();
      }
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}

/***************Confinamiento*****************/
void Confinement() 
{
  flag = 0;
  while (flag == 0) 
  {
    L_val = digitalRead(L_pin); //Leer el valor del sensor izquierdo
    M_val = digitalRead(M_pin); //Leer el valor del sensor intermedio
    R_val = digitalRead(R_pin); //Leer el valor del sensor derecho
    if ( L_val == 0 && M_val == 0 && R_val == 0 ) //Avanzar cuando no se detectan líneas negras   
    {    
        Car_front();
    }
    else 
    { 
      Car_back();
      delay(700);
      Car_left();
      delay(800);
    }
    if (Serial.available())
    {
      ble_val = Serial.read();
      if (ble_val == 'S') 
      {
        flag = 1;
        Car_Stop();
      }
    }
  }
}


/***************matriz de puntos******************/
//esta función se usa para la visualización de la matriz de puntos
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();  //usar la función para comenzar a transmitir datos
  IIC_send(0xc0);  //seleccionar una dirección
  for (int i = 0; i < 16; i++) //los datos de imagen tienen 16 caracteres
  {
    IIC_send(matrix_value[i]); //datos para transmitir imágenes
  }
  IIC_end();   //finalizar la transmisión de datos de imágenes
  IIC_start();
  IIC_send(0x8A);  //mostrar control y seleccionar ancho de pulso 4/16
  IIC_end();
}

//la condición para que los datos comiencen a transmitirse
void IIC_start()
{
  digitalWrite(SDA_Pin, HIGH);
  digitalWrite(SCL_Pin, HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin, LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin, LOW);
}

//transmitir datos
void IIC_send(unsigned char send_data)
{
  for (byte mask = 0x01; mask != 0; mask <<= 1) //cada carácter tiene 8 dígitos, que se detectan uno a uno
  {
    if (send_data & mask)  //establecer niveles altos o bajos según cada bit (0 o 1)
    {
      digitalWrite(SDA_Pin, HIGH);
    } 
    else 
    {
      digitalWrite(SDA_Pin, LOW);
    }
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, HIGH); //elevar el pin de reloj SCL_Pin para finalizar la transmisión de datos
    delayMicroseconds(3);
    digitalWrite(SCL_Pin, LOW); //bajar el pin de reloj SCL_Pin para cambiar las señales de SDA 
  }
}

//la señal de que la transmisión de datos ha terminado
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

/***************funcionamiento del motor****************/
void Car_back() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(back);  //mostrar la imagen de retroceso
}

void Car_front() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(front);  //mostrar la imagen de avance
}

void Car_left() 
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 255 - speeds_R);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, speeds_L);
  matrix_display(left);  //mostrar la imagen de giro a la izquierda
}

void Car_right() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, speeds_R);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 255 - speeds_L);
  matrix_display(right);  //mostrar la imagen de giro a la derecha
}

void Car_Stop() 
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
  matrix_display(STOP01);  //mostrar la imagen de parada
}
```

#### (5)Resultado de la prueba

Antes de cargar el código del programa, es necesario retirar el módulo Bluetooth; de lo contrario, la carga del código fallará.

Después de cargar el código correctamente, active los servicios de ubicación en su dispositivo y luego conecte el módulo Bluetooth.

Una vez que el módulo Bluetooth esté conectado y encendido, y la APP móvil se haya conectado correctamente al Bluetooth, podemos usar la APP móvil para controlar el robot tanque.

También puede controlar el robot con el control remoto.

![](media/13656cfee75dc5acbeba18a90a084e159.jpg)