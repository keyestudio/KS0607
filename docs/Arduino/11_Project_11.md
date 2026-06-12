### Proyecto 11: Tanque Seguidor Ultrasónico


#### **(1)Descripción:**

En la lección anterior, aprendimos sobre el carro inteligente seguidor de luz. En esta lección, podemos combinar los conocimientos para fabricar un carro seguidor de sonido ultrasónico. 

En el proyecto, usamos sensores ultrasónicos para detectar la distancia entre el carro y el obstáculo al frente, y luego controlar la rotación de los dos motores basándonos en estos datos para así controlar los movimientos del carro inteligente.

La lógica específica del carro inteligente seguidor de sonido ultrasónico se muestra en la tabla a continuación:

|                        Detección                        |              Configuración              |
| :-----------------------------------------------------: | :-------------------------------: |
| La distancia (cm) entre el carro y el obstáculo al frente | Establecer el ángulo del servo a 90° |
|                      **Condición**                      |           **Movimiento**            |
|               distancia≥20 y distancia≤50               |             Avanzar              |
|            10＜distancia＜20<br/>distancia＞50            |               Detenerse                |
|                       distancia≤10                       |              Retroceder              |

#### **(2)Diagrama de flujo:**

![](media/wps9.png)

#### **(3)Diagrama de conexión:**

![](media/72a10097d286bc5f9589df031b60484a.png)

#### **(4)Código de prueba:**

(<span style="color: rgb(255, 76, 65);">**Nota:**</span> No conecte el módulo Bluetooth antes de cargar el código, porque la carga del código también utiliza comunicación serial, y puede haber conflictos con la comunicación serial Bluetooth, lo que puede causar que la carga falle.)

```C
/*
  Keyestudio Mini Tank Robot V3 (Popular Edition)
  lesson 11
  Ultrasonic follow tank
  http://www.keyestudio.com
*/
#define servoPin 10  //El pin del servo

#define ML_Ctrl 4  //Define el pin de control de dirección del motor izquierdo
#define ML_PWM 6   //Define el pin de control PWM del motor izquierdo
#define MR_Ctrl 2  //Define el pin de control de dirección del motor derecho
#define MR_PWM 5   //Define el pin de control PWM del motor derecho
#define Trig 12
#define Echo 13
float distance;

void setup() 
{
  pinMode(servoPin, OUTPUT);
  pinMode(Trig, OUTPUT);
  pinMode(Echo, INPUT);
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  procedure(90); //Establece el ángulo del servo a 90°
  delay(500); //retardo de 500ms
}

void loop() 
{
  distance = checkdistance();  //Asigna la distancia medida por ultrasonido a distance
  if (distance >= 20 && distance <= 50) //avanzar
  {
    Car_front();
  }
  else if (distance > 10 && distance < 20)  //detenerse
  {
    Car_Stop();
  }
  else if (distance <= 10)  //retroceder
  {
    Car_back();
  }
  else  //En otras condiciones, se detiene
  {
    Car_Stop();
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

//La función para controlar servos
void procedure(byte myangle) 
{
  int pulsewidth;
  for (int i = 0; i < 5; i++) 
  {
    pulsewidth = myangle * 11 + 500;  //Calcula el valor del ancho de pulso    digitalWrite(servoPin, HIGH);
    delayMicroseconds(pulsewidth);   //El tiempo en nivel alto representa el ancho de pulso
    digitalWrite(servoPin, LOW);
    delay((20 - pulsewidth / 1000));  //Como el ciclo es de 20ms, el tiempo restante está en nivel bajo
  }
}
//La función para controlar el ultrasonido
float checkdistance() 
{
  static float distance;
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

#### **(5)Resultados de la prueba:**

Cargue el código de prueba exitosamente, realice las conexiones, deslice el interruptor DIP hacia el extremo derecho, encienda el dispositivo y establezca el servo a 90°, el carro inteligente sigue al obstáculo para moverse.

![](./media/img-20240117090457.png)