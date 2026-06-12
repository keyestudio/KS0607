### Proyecto 12: Tanque con Evasión de Obstáculos por Ultrasonidos

![](./media/image-20250709112200577.png)


#### **(1)Descripción:**

En el proyecto anterior, creamos un coche inteligente seguidor de sonido ultrasónico. En realidad, usando los mismos componentes y el mismo método de cableado, solo necesitamos cambiar el código de prueba para convertirlo en un coche inteligente de evasión de obstáculos por ultrasonidos. Este coche inteligente puede moverse con el movimiento de las manos humanas.

Usamos sensores ultrasónicos para detectar la distancia entre el coche inteligente y el obstáculo que tiene enfrente, y luego controlamos la rotación de los dos motores basándonos en estos datos para controlar los movimientos del coche inteligente.

|                          Detección                           |        |
| :----------------------------------------------------------: | :----: |
| Distancia medida por el sensor ultrasónico entre el coche y el obstáculo al frente <br />（establecer el ángulo del servo a 90°） | a(cm)  |
| Distancia medida por el sensor ultrasónico entre el coche y el obstáculo a la derecha <br />（establecer el ángulo del servo a 20°） | a2(cm) |
| Distancia medida por el sensor ultrasónico entre el coche y el obstáculo a la izquierda <br />（establecer el ángulo del servo a 160°） | a1(cm) |
|   **Configuración:** establecer el ángulo inicial del servo a 90°    |        |

|   Condición 1   |        Condición 2         | Condición 3 | Movimiento                                                     |
| :-------------: | :------------------------: | ----------- | ------------------------------------------------------------ |
|      a＜20      |                            |             | Detener durante 500ms；<br />establecer el ángulo del servo a 180°, leer a1, retraso de 100ms；<br />establecer el ángulo del servo a 0°, leer a2, retraso de 0.1s. |
|                 | a1＜50<br />o<br />a2＜50 |             | Comparar a1 con a2                                           |
|                 |                            | a1＞a2      | Establecer el ángulo del servo a 90°, girar a la izquierda durante 700ms (establecer PWM a 255)<br />avanzar（establecer PWM a 200）. |
|                 |                            | a1＜a2      | Establecer el ángulo del servo a 90°, girar a la derecha durante 700ms (establecer PWM a 255) <br />avanzar（establecer PWM a 200）. |
| **Condición 1** |      **Condición 2**       |             | **Movimiento**                                                 |
|      a＜20      | a1≥50<br />y<br />a2≥50  | Aleatorio      | establecer el ángulo del servo a 90°, girar a la izquierda durante 500ms (establecer PWM a 255)<br />avanzar (establecer PWM a 200)<br /><br />establecer el ángulo del servo a 90°, girar a la derecha durante 500ms (establecer PWM a 255) <br />avanzar (establecer PWM a 200) |
|  **Condición**  |                            |             | **Movimiento**                                                 |
|      a≥20       |                            |             | avanzar (establecer PWM a 100)                                 |



#### **(2)Diagrama de flujo:**

![](media/wps10.png)

#### **(3)Diagrama de conexión:**

![](media/72a10097d286bc5f9589df031b60484a.png)

(<span style="color: rgb(255, 76, 65);">Nota:</span> los cables marrón, rojo y naranja del servo están conectados respectivamente a G (GND), V（5V）y D10 de la placa de expansión；y para el sensor ultrasónico, el pin VCC está conectado a 5v (V), el pin Trig al digital 12 (S), el pin Echo al digital 13 (S), y el pin Gnd a Gnd (G); igual que en el proyecto anterior.）

#### **(4)Código de prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también usa comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 12
  Ultrasonic avoid tank
  http://www.keyestudio.com
*/
#define servoPin 10  //El pin del servo
int a, a1, a2;
#define ML_Ctrl 4  //Definir el pin de control de dirección del motor izquierdo
#define ML_PWM 6   //Definir el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  //Definir el pin de control de dirección del motor derecho
#define MR_PWM 5   //Definir el pin de control PWM del motor derecho
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  Serial.begin(9600);
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //Establecer el ángulo del servo a 90°
  delay(500); //retraso de 500ms
}

void loop() 
{
  a = checkdistance();  //Asignar la distancia al frente detectada por el sensor ultrasónico a la variable a

  if (a < 20) //Cuando la distancia al frente es menor de 20cm
  {
    Car_Stop();  //El robot se detiene
    delay(500); //retraso de 500ms
    procedure(180);  //El pan-tilt ultrasónico gira a la izquierda
    delay(500); //retraso de 500ms
    a1 = checkdistance();  //Asignar la distancia a la izquierda detectada por el sensor ultrasónico a la variable a1
    delay(100); //leer valor
    procedure(0); //El pan-tilt ultrasónico gira a la derecha
    delay(500); //retraso de 500ms
    a2 = checkdistance(); //Asignar la distancia a la derecha detectada por el sensor ultrasónico a la variable a2
    delay(100); //leer valor
    
    procedure(90);  //Volver a 90°
    delay(500);
    if (a1 > a2) 
    { //Cuando la distancia a la izquierda es mayor que a la derecha
      Car_left();  //El robot gira a la izquierda
      delay(700);  //girar a la izquierda 700ms
    } 
    else 
    {
      Car_right(); //Gira a la izquierda durante 700ms
      delay(700);
    }
  } 
  else//Cuando la distancia al frente es >=20cm, el robot avanza
  {    
    Car_front(); //avanzar
  }

}

void Car_front()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_back()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_left()
{
  digitalWrite(MR_Ctrl, HIGH);
  analogWrite(MR_PWM, 55);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 200);
}

void Car_right()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 200);
  digitalWrite(ML_Ctrl, HIGH);
  analogWrite(ML_PWM, 55);
}

void Car_Stop()
{
  digitalWrite(MR_Ctrl, LOW);
  analogWrite(MR_PWM, 0);
  digitalWrite(ML_Ctrl, LOW);
  analogWrite(ML_PWM, 0);
}

//La función controla los servos
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Calcular el valor del ancho de pulso
    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //El tiempo en nivel alto representa el ancho de pulso
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //Como el ciclo es de 20ms, el tiempo restante está en nivel bajo
  }
}

//La función controla el ultrasonido
float checkdistance() 
{
  float distance;
  digitalWrite(Trig, LOW);
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(Trig, LOW);
  distance = pulseIn(Echo, HIGH) / 58.20;  //El 58.20 aquí proviene de 2*29.1=58.2
  delay(10);
  return distance;
}
```

#### **(5)Resultado de la prueba:**

Después de cargar el código de prueba con éxito, realizar el cableado, cambiar el interruptor DIP al extremo ON y encender, el coche inteligente avanza y evita obstáculos automáticamente.

![](./media/img-20240117090420.png)